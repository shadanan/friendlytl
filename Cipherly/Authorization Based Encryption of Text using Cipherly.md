# Intro

In a previous video, I introduced Cipherly, an app for encrypting messages using a password. Over the past couple of weeks, I've been working on a new feature in Cipherly that enables authorization based encryption. The idea is, if I want to send Alice a secret message, I can encrypt the message, and authorize Alice using her email address. Then, in order for Alice to decrypt the message, she would first login using her email, and then Cipherly would decrypt the message if the login was successful. All of this happens without sending the secret message to Cipherly. The whole process involves a technique called envelope encryption.

# Envelope Encryption

So, let's learn a little bit about envelope encryption.

Let's say that I have a secret message that I only want Alice to be able to read. The first step is to have my browser generate an encryption key locally. We use this key to encrypt our secret message for Alice. Now, since this key is used to encrypt the data, we call it the Data Encryption Key, or DEK. Next, we send the DEK, and Alice's email address to the server, Cipherly. Cipherly then bundles the DEK and Alice's email address together into an envelope. Cipherly then encrypts the envelope using its own encryption key. Since this key is used to encrypt the DEK, which is also a key, we call it the Key Encryption Key, or KEK. Cipherly then returns the encrypted envelope to me. My browser then takes the KEK encrypted envelope, and our DEK encrypted secret message, and bundles them together. This is my payload, which I send to Alice.

When Alice wants to decrypt the message, she goes to Cipherly. Cipherly then prompts her to login. Currently, Cipherly only supports OAuth2 with Google. In the process of logging in, Alice will get a token, that asserts her identity. Next, Alice will provide the payload to her browser. The browser will then split the KEK encrypted envelope, and the DEK encrypted secret message. The browser will then ask Cipherly to decrypt the KEK encrypted envelope, passing Oauth2 token. Cipherly will then use the KEK to decrypt the envelope, and check to see if Alice appears as one of the authorized users in the envelope. If yes, then Cipherly returns the decrypted DEK. The browser then uses the DEK to decrypt the secret message.

# Demo

Okay, enough talk, let's fight. I mean, let's demo!

```python codeanim
chrome.activate()
chrome.navigate("cipherly.app")
```

So, suppose Alice wants to send me a secret message. She heads over to Cipherly's auth based encryption tab, types out her secret message, and then authorizes me using my email address. Then she clicks encrypt and send me the encrypted payload URL.

I can then follow the URL which takes me to Cipherly. In order to decrypt, Cipherly requires me to login. Once I login, I can click the Decrypt button, and I can then read Alice's secret message.

# Deep Dive

Coming up next is a deep dive into the code. Hold on to your hats!

## Encryption

When the Encrypt button is clicked, this function is called, and the contents of the plaintext and authorized users are passed as arguments.

Then, we generate the Data Encryption Key and Initialization Vector using SubtleCrypto locally in the browser. Also locally in the browser, we encrypt the plaintext using the DEK and the Initialization Vector.

Next, we call Cipherly.kekEncrypt to encrypt the DEK, the Initialization Vector, and the authorized emails. If we look at the kekEncrypt method, we can see that we are calling fetch to our API, and we pass the base64 encoded DEK, initialization vector and authorized emails.

Finally, we combine the KEK encrypted DEK and the DEK encrypted ciphertext into the final payload and return it.

## Decryption

So that was encryption. Let's take a look at decryption.

# Outro

Cipherly is currently available at cipherly.app. The source code is MIT licensed and available on GitHub. As usual, relevant links are in the description.

Cipherly is still a work in progress, and should probably not be used for real secrets. Even though I've been working professionally in the security industry for a while, it's easy to misuse crypto libraries. I would want to get an external audit of Cipherly before I can claim that it's safe to use.

If you like Cipherly and have ideas for its improvement, drop your suggestions in the comments. More ways to encrypt and decrypt are coming soon. Make sure you're subscribed so that you don't miss those updates. And while you're at it, hit those other buttons too.

Thanks for watching, and I'll see you in the next one!
