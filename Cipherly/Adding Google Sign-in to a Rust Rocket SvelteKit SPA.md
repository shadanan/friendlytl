# Intro

In a previous video, I added authorization based encryption to Cipherly. Cipherly is an app that makes it easy to share secrets with others over public channels. For example, if you want to share a secret with Alice, you can use Cipherly to encrypt a message using Alice's email address. Then you can send Alice the Cipherly payload over slack for example. In order for Alice to decrypt the payload, she will need to first authenticate with Cipherly. Authentication with Cipherly currently uses Sign-in with Google.

In this video, we'll explain how Sign-in with Google works by adding it to the Time Getter webapp. Time Getter is a SvelteKit webapp I created in a previous video that fetches the time from a server that we wrote in Rust using the Rocket web framework. Using Sign-in with Google, our Rocket server will be able to know the identity of the user that is trying to fetch the time.

Ok, let's get started!

# Roadmap

Here's the roadmap to get Sign-in with Google to work.

Initially:

1. In the browser, the user signs-in using their Google account and is issued a token.
2. And the server fetches Google's public certs.

Then, for every subsequent request to the server:

1. The user calls our server's get time endpoint passing their Google token.
2. The server validates the token using Google's public certs.
3. If validation succeeds, the server returns the time, otherwise, it returns an unauthorized error.

# Demo

Alright, enough talk, let's demo!

Here's the Time Getter app. Currently, we're not logged in. If we click the Get Time button, we get a 401 Unauthorized error. Ok. Let's login. And now, let's click the Get Time button again. This time, we see a welcome message, and our current time.

# Deep Dive

So, how does it work?

## Oauth 2.0 Client IDs

Well, before we start, we need to configure our OAuth consent screen, and create an OAuth2 client ID. Time Getter is reusing Cipherly's OAuth configuration and client ID. To do this for your app, navigate to the Google API Console page, configure your OAuth consent screen. Then, go to the Credentials page and create a new OAuth client ID. Give it a name, and set the authorized JavaScript origins. It should look something like this. The value here is the Client ID.

## JWT

In our client code, we use the `google-oauth-gsi` library to create the Sign-in with Google button. Copy paste the Client ID here. When the user's login succeeds, we will get a Json Web Token, also known as a JWT.

```jwt
eyJhbGciOiJSUzI1NiIsImtpZCI6IjkzYjQ5NTE2MmFmMGM4N2NjN2E1MTY4NjI5NDA5NzA0MGRhZjNiNDMiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmdvb2dsZS5jb20iLCJhenAiOiI5ODEwMDIxNzU2NjItZzhqcjJuODlicHRzbjhuOWRzMWZuNWVkZmhlb2pyN2kuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJhdWQiOiI5ODEwMDIxNzU2NjItZzhqcjJuODlicHRzbjhuOWRzMWZuNWVkZmhlb2pyN2kuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJzdWIiOiIxIiwiZW1haWwiOiJmcmllbmRseXRsQGVtYWlsLmNvbSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJuYmYiOjE3MTI3OTM5NDIsIm5hbWUiOiJGcmllbmRseSBUTCIsInBpY3R1cmUiOiJodHRwczovL2xoMy5nb29nbGV1c2VyY29udGVudC5jb20vYS9BQ2c4b2NJUmZsMU1KcmRLRl9WOGU0NlNRaWptRnpzMUpvRWFRTG9nQ3NPRUlZQy1UMkhrMnhjUEt3PXM5Ni1jIiwiZ2l2ZW5fbmFtZSI6IkZyaWVuZGx5IiwiZmFtaWx5X25hbWUiOiJUTCIsImlhdCI6MTcxMjc5NDI0MiwiZXhwIjoxNzEyNzk3ODQyLCJqdGkiOiI1ZjM4NmQ0MTQwMGQwNWVkNTg2NzgzMWFmYjk2ODUxOGIyZGIyMzM0In0.M30D9YGSBR-I0qknzMTLWezlUIxXsz7dYrIsH_rvmuglzmvsCKFmC_DTjJZlgGSVqBOcmB-TXop6fd0dcOOMgBYeymXJGbIUe3W9EPHwuWb6oP8w7sQ14sGQnjmJunX9tJqzKNuGHK9tUz9Q3ufu83xVC9djcNMB_9sUe6sPeruHL2THmv-NeA7Cbaj7o1hDgjTkLz5b1OrOxoJW62DSWcm6rOQdj_-MbriwvmegSq5E4kBkCCCULgIC9fLi8Lu9l3Mr4epScoo6injxHeEApI9u9I-Yvd1oE3Bug0mfIGLyQDs_30uXlTsWecBJQPZsJgKtNPvrL34FGhpZAbrQKw
```

Here's an example JWT. It consists of three parts, the header, the payload, and the signature. The header has information about what algorithm is used, and a `kid` field which identifies the key that was used to sign the token.

The payload contains a set of claims from Google's auth server. If the token's signature is valid, then we can trust that the claims have not been tampered with.

## Google Certs

Tokens that use the RS256 algorithm, are signed using the private key of public/private key pair. We can validate the token if we have the public key. For now, this is all you need to know, but if you're especially curious, here's the details.

Google produces the signature, by using their private key to encrypt the hash of the token's header and payload. We can validate the token by decrypting the token's signature using Google's public key. Then we compute the same hash ourselves, and compare it to the the one we decrypted from Google. If they are equal, then the token was not tampered with.

```
https://www.googleapis.com/oauth2/v3/certs
```

So, in order to validate the token, we need Google's public key. We can get it at this URL. In this case, there are two public keys. The one that was used to sign our JWT is the one where the `kid` matches token's `kid`.

Our Rocket server needs to get these keys. So, in Rust, we have a fetch function that uses the reqwest library to make a call to the Google public keys URL. This function is called at startup and these keys will be made available to every call to our server.

## Fetch Time

Now, when the user click's the Get Time button, the fetchTime function gets called, and we pass the JWT as an authorization bearer token.

This calls our time function in Rust. The time function takes this claims argument, which is produced by this Rust request guard. The purpose of the request guard is to validate the JWT.

So here are the validation steps. First, we get Google's public keys. Then, we extract the Authorization header from the request. If that fails, we return unauthorized. Then we extract the bearer token, parse the header, and get the `kid` that signed the token. If anything fails, unauthorized. Once we have the `kid`, we can get the corresponding Key from Google's public keys. Then we call decode, which validates the bearer token using Google's public key, as well as a list of expected claims. In our case, we ensure that the algorithm is RS256, the audience is this thing, and the issuer is Google. If that succeeds, we return the decoded claims, which in our case includes the user's email, name, and token expiration time.

Back in our time function, we return the time along with a little greeting saying hello to the authenticated user.

# Outro

Time Getter, and the pull request that introduces Sign-in with Google is MIT licensed and is available on GitHub. As usual, relevant links are in the description.

If you liked this video, hit the thumbs up. I'm The FriendlyTL and I make useful open sources apps such as Cipherly, CodeAnim, and Hexly. If you're interested in the apps that I make and maintain, subscribe! Thanks for watching, and I'll see you in the next one!
