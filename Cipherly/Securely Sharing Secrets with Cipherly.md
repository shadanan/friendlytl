# Intro

Cipherly is a free and open source webapp that allows you to securely share a secret with someone else.

I've just added support for file encryption. So, for example, suppose you have a spreadsheet in CSV format that contains sensitive user data like names and emails that you'd like to share with me. Cipherly can encrypt the CSV file without having access to the file. And Cipherly can ensure that only I will be able to decrypt it.

I'm going to structure the rest of this video as a Q&A. Let's go!

## How do I use Cipherly?

Alright. Demo time!

```python codeanim show-sensitive
click((1115, 225))
tap(Key.space)
pause(2)
tap(Key.space)
```

So, in this folder, we have our unencrypted CSV file. You can see that it contains some sensitive user data. It's not real data, of course! I asked ChatGPT to generate some fake sensitive data for me.

```python codeanim encrypt
chrome.activate()
chrome.navigate("https://cipherly.app/")
click((410, 310))  # Encrypt tab
```

Now, let's say that you want to encrypt this file so that only friendlytl@gmail.com can decrypt it. So, first, you go to https://cipherly.app and then click on the Encrypt tab.

```python codeanim encrypt-drag
drag((1115, 225), (475, 570))  # File to Cipherly
click((472, 686))  # Email field
write("friendlytl@gmail.com\n")
click((110, 820))  # Encrypt button
click((640, 620))  # Save button
```

Next, you'll drag sensitive.csv here. Then you'll authorize friendlytl@gmail.com by typing his email address here. Finally, you click on the Encrypt button, and save the encrypted CSV file to your computer.

```python codeanim reset
wait()
# Clear downloads
# Close tabs
# Switch to Cipherly Decrypt folder
# Reconfigure downloads to Decrypt folder
```

Now, you send me the encrypted CSV file, sensitive.csv.cly.

```python codeanim show-encrypted
click((1115, 225), count=2)
click((905, 646))  # Open Anyway
click((672, 136))  # Text Editor
pause(1)
click((260, 89))  # Close
```

Once I receive this file, if I try to open it, I'll see some of the unencrypted header, but most of the file is all gibberish.

```python codeanim encrypt
chrome.activate()
chrome.navigate("https://cipherly.app/")
click((574, 310))  # Decrypt tab
drag((1115, 225), (475, 570))  # File to Cipherly
wait()  # Modify email address
move((475, 570))
click((145, 530))  # Sign-in as Shad
wait()  # Modify email address and name
move((145, 530))
click((1240, 706))  # Click Shad Sharma
wait()  # Modify Logged in as Shad Sharma
move((1240, 706))
click((110, 600))  # Click Decrypt
click((640, 620))  # Save button
pause(2)
```

To decrypt the file, I go to https://cipherly.app and then click on the Decrypt tab. Next I'll drag the encrypted file here. Cipherly then prompts me to login. Once I've logged in, I click on the Decrypt button, and save the decrypted CSV file to my computer.

```python codeanim show-decrypted
click((1415, 225))
tap(Key.space)
pause(2)
tap(Key.space)
```

I can then open the decrypted CSV file and see the sensitive data.

## How can Cipherly encrypt your data without having access to the data?

This is done using a technique known as Envelope Encryption. Basically, instead of Cipherly encrypting your sensitive CSV file, _you_ instead encrypt the file yourself using your own encryption key. Cipherly then encrypts just your key.

## How does Cipherly ensure that only I can decrypt the data?

When you ask Cipherly to encrypt your key, you also tell Cipherly who is authorized to view the CSV file. When I go to decrypt the CSV file, Cipherly will validate my identity using a trusted third party, Google in our case. Google returns to me a token that asserts my email address. I present this token to Cipherly and if I am one of the authorized users, Cipherly will return the encryption key to me which I can use to decrypt the CSV file. The process of validating my identity with a third party is known as Oauth2.

## Who made Cipherly?

I was a little surprised when people asked me this question. I kinda thought that it was clear that I made it. Well, in any case, that's the answer. The answer is me. The FriendlyTL made Cipherly.

## Why did you make it?

For fun, mostly. I left my job earlier this year to start doing what I really love. I want to make useful open source tools that genuinely help people. But there's no point in making things in a vacuum. People need to know about it. So, I'm here on YouTube making videos as well, so that people can learn about my freely available tools.

## Who is Cipherly for?

If you need the services that Cipherly provides, you already know it. The situation where you have some sensitive data that you want to share with someone else tends to come up in corporate settings. Often there are policies in place that govern who should have access to what kind of data, but no tools in place that actually enforce those policies. In these situations, you can use Cipherly share data with someone while being compliant with the policy.

## Has Cipherly had a security audit?

Not yet! But I'm in contact with some former colleagues who can help me with this. Subscribe to my channel so that when I do get Cipherly audited, you'll be notified!

# Outro

Cipherly is currently available at cipherly.app. The source code is MIT licensed and available on GitHub. As usual, relevant links are in the description.

I'm The FriendlyTL and I make edutainment videos about software and open source apps that I also make. If you liked this video, hit the thumbs up. And if you're interested in this kind of content, consider subscribing. Thanks for watching; I'll see you in the next one!
