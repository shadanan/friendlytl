# Intro

Over the past few weeks, I've been working on a tool called Cipherly. Cipherly is a webapp that uses SubtleCrypto to encrypt and decrypt text in the browser without sending the text to the server. Once a message is encrypted, it can be sent to someone else. And if they know the password, they can decrypt it! Let's take a look!

# Demo

```python codeanim
chrome.activate()
chrome.navigate("cipherly.app")
```

Cipherly is live and is hosted at cipherly.app. If you navigate there, you'll land on the homepage which currently looks like this.

```python codeanim
tap(Key.tab, repeat=2)
tap(Key.enter)
```

Let's start by encrypting a secret. So, we'll click on the Encrypt button.

```python codeanim
chrome.toggle_devtools()
tap(Key.tab, repeat=14)
```

And we'll open the dev tools so that we can observe network traffic.

```python codeanim
tap(Key.tab, repeat=3)
write("The answer to the meaning of life, the universe, and everything, is 42.")
```

Then, in the plaintext text box, let's type our secret message.

```python codeanim
tap(Key.tab)
write("hunter2")
```

And then encrypt the message using our password, `hunter2`.

```python codeanim
tap(Key.tab)
tap(Key.enter)
```

And then we'll click on the Encrypt button. This text here is the envelope containing the ciphertext. And notice that no network activity was recorded. So the secret never left the browser!

Now, let's say that I want to send this secret to Alice.

```python codeanim
tap(Key.tab, repeat=3)
tap(Key.enter)
```

We can click the Copy Decrypt URL button and then paste the URL in an email and send it to Alice.

```python codeanim alice
chrome.new_tab()
chrome.toggle_devtools()
tap("l", modifiers=[Key.cmd])
tap("v", modifiers=[Key.cmd])
tap(Key.enter)
```

Alice would then open the link in her browser.

Take a look at the URL and notice that the ciphertext is encoded in the URL as a hash. Compare that to the request in the Network tab. Notice that by encoding it this way, the secret ends up not being a part of the request and so it's not sent to the server.

Alice clears the network tab and proceeds to decrypt the secret.

```python codeanim
tap(Key.tab, repeat=5)
write("hunter2")
```

She'll type the same password, `hunter2`.

```python codeanim
tap(Key.tab)
tap(Key.enter)
```

And then click the Decrypt button. And there's the decrypted secret, all with no network traffic!

If you'd like to try out Cipherly, head over to cipherly.app.

# Deep Dive

Coming up next is a deep dive into the code. Hold on to your hats! Cipherly uses SubtleCrypto, which is built-in to most modern browsers.

## Encryption

When the Encrypt button is clicked, this function is called. And the contents of the plaintext and password boxes are passed as the plaintext and password arguments.

### Derive Key

Then, on line 18, we call `deriveKey`. This function derives the crypto key that will be used to encrypt. Given a password and a salt, `deriveKey` will always return the same key. Notice that it also takes a salt which was generated on the previous line. The purpose of the salt is to make it difficult for an adversary to use a dictionary attack.

Here's my implementation of `deriveKey`. The first step is to use SubtleCrypto's `importKey` function to generate the `keyMaterial` which is based on the password using the PBKDF2 algorithm. Next we use SubtleCrypto's `deriveKey` function to derive a symmetric AES-GCM key from the `keyMaterial`. And here, we specify 100000 iterations. The purpose of this is to make it computationally expensive to brute force the key. We can make it more computationally expensive by increasing the number of iterations.

### Encrypt

Back in Cipherly's encrypt function, on line 21, we call encrypt. This function encrypts the plaintext using the derived key. It also takes an initialization vector which was generated on the previous line.

Here's the implementation. It's straightforward. We call SubtleCrypto's encrypt function. We configure it to use the symmetric AES-GCM encryption algorithm. Here's the initialization vector, and our derived key. And this last argument is the data we want encrypted.

### Encode

Finally, on line 27, we encode the salt, the initialization vector, and the encrypted ciphertext into an envelope.

Here's the implementation, which takes a PasswordEnvelope object. We then use MessagePack to pack the binary data, and then base64 encode it in a way that is safe to use in a URL.

## Decryption

So that was encryption. Let's take a look at decryption. So, when the user lands on the decrypt page, this if statement is run. It checks if a hash exists in the URL. And if it does, it populates the Ciphertext Envelope field with the fragment.

When the user clicks on Decrypt, this function is called, and the contents of the envelope and password are passed as arguments.

We're now doing the reverse of the steps we did in encryption. First we base64 decode and unpack the envelope. And we get back the salt, initialization vector, and ciphertext.

Then we re-derive the encryption key from the password which the user supplied, and the salt, which was in the envelope.

Finally, we decrypt the ciphertext using the derived key and the initialization vector, and return it as a string.

# Outro

Congrats on making it this far. That code was pretty dense. Cipherly is currently available at cipherly.app. The source code is MIT licensed and available on GitHub. As usual, the relevant links are in the description.

Cipherly is very much a work in progress, and should probably not be used for real secrets. Even though I've been working professionally in the security industry for a while, it's easy to misuse crypto libraries. I would want to get an external audit of Cipherly before I can claim that it's safe to use.

If you like Cipherly and have ideas for its improvement, drop your suggestions in the comments. I personally have some awesome features that I plan to add. Make sure you're subscribed so that you don't miss those updates. And while you're at it, hit those other buttons too.

Thanks for watching, and I'll see you in the next one!
