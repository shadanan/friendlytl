# Intro

In a previous video, I introduced Cipherly, an app for encrypting messages using a password. Over the past couple of weeks, I've been working on a new feature in Cipherly that enables authorization based encryption. The idea is, if I want to send Alice a secret message, I can encrypt the message, and authorize Alice using her email address. Then, in order for Alice to decrypt the message, she would first login using her email, and then Cipherly would decrypt the message if the login was successful. All of this happens without sending the secret message to Cipherly. The whole process involves a technique called envelope encryption.

So, let's learn a little bit about envelope encryption.

# Envelope Encryption

Let's say that Alice has a secret message that she only wants me to be able to read. The first step is to have Alice's browser generate an encryption key locally. She then uses this key to encrypt her secret message for me. Now, since this key is used to encrypt the data, we call it the Data Encryption Key, or DEK. Next, she sends the DEK, and my email address to the Cipherly server. Cipherly bundles the DEK and my email address together into an envelope. Cipherly then encrypts the envelope using its own encryption key. Since this key is used to encrypt the DEK, which is also a key, we call it the Key Encryption Key, or KEK. Cipherly then returns the encrypted envelope to Alice. Alice's browser then takes the KEK encrypted envelope, and her DEK encrypted secret message, and bundles them together. This is the payload, which Alice sends to me.

When I want to decrypt the message, I go to Cipherly. Cipherly then prompts me to login. Currently, Cipherly only supports OAuth2 with Google. In the process of logging in, I will get a token, that asserts my identity, signed by Google. Next, I will provide the payload to my browser. The browser will then split the payload into the KEK encrypted envelope, and the DEK encrypted secret message. The browser will then ask Cipherly to decrypt the KEK encrypted envelope, passing my Google Oauth2 token. Cipherly will then validate the token, and use the KEK to decrypt the envelope. It will also check to see if my email appears as one of the authorized users in the envelope. If yes, then Cipherly returns the decrypted DEK. My browser then uses the DEK to decrypt the secret message.

Now, suppose that Eve intercepts the encrypted payload. If she tries to decrypt the message, when Cipherly receives the KEK encrypted envelope and Eve's Oauth2 token, Cipherly will see that Eve's email address does not appear as one of the authorized users, and will return a 401 unauthorized error. Now suppose that Eve is very enterprising and tries to spoof a token that contains my email address. If she sends her spoofed token to Cipherly, Cipherly will detect that the token was not signed by the Google Oauth2 token provider and will return a 401 unauthorized error.

# Demo

Okay, enough talk, let's fight. I mean, demo!

```python codeanim encrypt
chrome.activate()
chrome.navigate("cipherly.app")
tap(Key.tab, repeat=4)
tap(Key.enter)
pause()
tap(Key.tab, repeat=7)
tap(Key.end)
write("Username: AzureDiamond\nPassword: hunter2")
tap(Key.tab)
write("shadanan@gmail.com\n")
tap(Key.tab, repeat=2)
pause()
tap(Key.enter)
tap(Key.end)
pause()
tap(Key.tab)
tap(Key.enter)
```

I'm Alice and I'd like to send a secret message to Shad. To do this, I head over to Cipherly's auth based encryption tab, and type my secret. Then I authorize Shad using his email address. Then I click the encrypt button and copy the encrypted payload URL. This payload is safe for anyone to see, so I can safely share the payload with Shad in our public slack channel.

```python codeanim decrypt
chrome.activate()
tap("l", modifiers=[Key.cmd])
paste("https://cipherly.app/auth/#gq5zZWFsZWRFbnZlbG9wZcSpkpxRzLVMX2g3YX3Mp8z-zOjM7dwAY8zLPczPZcy-zMwOzJcrWMzbL8yUI8yczMjMs8zpGmjMiMz2zPHMsBdsP8zoN3jM9l_M8nkWR0PM6AsRzPnM3nVMzI9nDMy9U8ybzITMgszuY8y9DiMVUEd9zNJtH8zCzMxgbAs0Ssz1zOLMrXdTTsykzITM2h3M_MyoesyNCMzYEn5INcz8zJXM18yVzN_M1czVPKpjaXBoZXJUZXh0xDh796Mqc51i1t5tpQS8TDTBkMwNpmu6IOip3iFNJPeZ1MPcFFfmQZ7pg3rUdk3alfg-ObLM0YbEKA")
tap(Key.enter)
pause()
tap(Key.tab, repeat=7)
tap(Key.enter)
pause()
tap(Key.tab)
tap(Key.enter)
pause()
tap(Key.tab, repeat=3)
tap(Key.end)
pause()
tap(Key.enter)
tap(Key.end)
```

Next, I click on the URL that Alice sent me, and it takes me to Cipherly. In order to decrypt, Cipherly requires me to login. Once I login, I can click the Decrypt button, and I can then read Alice's secret message.

# Deep Dive

Coming up next is a deep dive into the code. Hold on to your hats!

## Encryption

When the Encrypt button is clicked, this function is called, and the contents of the plaintext and authorized emails are passed as arguments.

Then, we generate the Data Encryption Key and Initialization Vector using SubtleCrypto locally in the browser. Then we encrypt the plaintext using the DEK and the Initialization Vector. This all done entirely in the browser without sending the plaintext to the server.

Next, we call seal to encrypt the DEK, the Initialization Vector, and the authorized emails, which produces our sealed envelope. If we look at the seal method, we can see that we are calling fetch to our API, and we pass the base64 encoded DEK, initialization vector and authorized emails. Notice that we are only sending the DEK to the server and the server never sees the plaintext, encrypted or otherwise.

Finally, we combine the KEK encrypted DEK, also known as the sealed envelope, and the DEK encrypted ciphertext into the final payload and return it.

## Decryption

So that was encryption. Let's take a look at decryption.

When the Decrypt button is clicked, this function is called, and the encrypted payload is passed as an argument.

We need to ensure that the current user is signed in. If not we throw an error.

Next, we extract the KEK encrypted DEK, and the DEK encrypted text from the payload.

Then we call unseal on the sealed envelope passing the user's token. Let's take a look at the unseal function. This function calls fetch to the unseal API, passing the user's token as the authorization header, and the base64 encoded sealed envelope.

The result contains the decrypted DEK and Initialization Vector, as well as the authorized emails.

Finally, we use the DEK and the Initialization Vector to decrypt the ciphertext, and return it.

# Outro

Cipherly is currently available at cipherly.app. The source code is MIT licensed and available on GitHub. As usual, relevant links are in the description.

Cipherly is still a work in progress, and should probably not be used for real secrets. Even though I've been working professionally in the security industry for a while, it's easy to misuse crypto libraries. I would want to get an external audit of Cipherly before I can claim that it's safe to use.

If you like Cipherly and have ideas for its improvement, drop your suggestions in the comments. More ways to encrypt and decrypt are coming soon. Make sure you're subscribed so that you don't miss those updates. And while you're at it, hit those other buttons too.

Thanks for watching, and I'll see you in the next one!
