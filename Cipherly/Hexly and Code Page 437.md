# CP437

When I was growing up, my dad had a 386 computer that I used play around on. We also had WordPerfect 5.1 installed on this computer, and I would sometimes use it to write up my assignments for school.

To start it, you would `cd` into the WP51 directory, and then run `wp`, and you'd be greeted with this very blue screen.

Something that really fascinated me as a kid was that I could press and hold the alt key on the keyboard, then type a number on the numpad, say 1, and this smiley face would appear.

- Alt-2 was a filled in variation of the smiley.
- Alt-3, 4, 5, and 6 was a heart, a diamond, a club, and a spade.

And it didn't stop there. I eventually learned that there were even more symbols available if I held alt and typed longer sequences of numbers. For example, Alt 130, 136, and 138 were various accented Es, useful for my french assignments. As a kid, I spent a lot of time typing random alt numbers just to see what I'd get. If you type Alt 1281, you get another smiley face. I was surprised that there were different ways that you could get the same symbol.

These alt sequences would also work in other programs. Like edit. We can type alt-1, 2, 3, 4, 5, 6 and we would get the familiar sequence.

As a kid, I was exploring a character encoding called code page 437 – the original character set of the IBM PC. This code page has a total of 256 code points and includes various arrows, symbols, punctuations and even some characters for building text based UIs. When I was typing alt sequences longer than 256, it was wrapping around. So for example, alt 257 would also be the smiley face. Let's save this file to the DosBox folder, so that we can use it later in this video!

I later discovered that there were other code pages that you could switch to. For example, here is code page 850, which is largely the same as code page 437, but opts to have some additional characters instead of the UI and mathematical symbols. The majority of these code pages have a couple things in common. They typically use one byte to encode one character, which is why they all have 256 code points. And they largely aim to be compatible with ASCII. That's why the characters in this range 0x20 to 0x7e are the same across code pages.

As PCs moved into the Windows-era, they started using the Windows-1252 code page, which altogether drops the text-mode UI characters.

Nowadays, UTF-8 is the most widely used character encoding. But, you can still create the characters from those older code pages. For example, in notepad, if we type Alt-1, and Alt-2, we get the smiley faces. If we type Alt 3, 4, 5, 6, we get heart, diamond, club, and spade. These are all being taken from Code Page 437. We can also produce characters from Windows-1252, by prefixing the alt sequence with a 0. So for example, to produce the copyright symbol, we need the decimal version of A9, which is 169. So, Alt-0169 is the copyright symbol.

Let's save this file to the WinBox folder. Notice that the default is to use UTF-8 encoding.

# Hexly

Anyway, the purpose of that story, aside from being interesting to me, is to introduce you to a little hex viewer that I made for Jupyter notebooks, called Hexly.

A hex viewer is a tool that enables you to see the contents and structure of binary data.

```python codeanim
chrome.activate()
write("\nimport hexly as hl")
tap(Key.enter, modifiers=[Key.shift])
```

We'll start by importing `Hexly`.

```python codeanim
write("hl.HexView(bytes(range(256)))")
tap(Key.enter, modifiers=[Key.shift])
```

Next, let's use Hexly to show a hex view of the bytes 0 through 255.

This area here shows you the bytes of the data. Each byte is represented by a hex value from 00 to FF, and every row shows 16 bytes at a time. This area over here shows the data decoded as ASCII. Hex viewers usually operate on files. Hexly is different in that it works in a Jupyter notebook instead.

```python codeanim
write('with open("WinBox/altchars.txt", "r") as f:\n')
write('winbox_data = f.read()')
tap(Key.enter, modifiers=[Key.shift])
```

So, in the previous section, we ended up creating two files. Let's open the file we created in the Windows box which we called `WinBox/altchars.txt`. We know this this file was encoded as UTF-8, so Python can directly decode it. We can read this file in text mode which is indicated by this `r` here.

```python codeanim
write('winbox_data')
tap(Key.enter, modifiers=[Key.shift])
```

And if we evaluate the variable, we get back the string we typed in Notepad.

```python codeanim
write('with open("DosBox/altchars.txt", "rb") as f:\n')
write('dosbox_data = f.read()')
tap(Key.enter, modifiers=[Key.shift])
```

The second file was saved to `DosBox/altchars.txt`. Now this file was not encoded in UTF-8, so when we open it, we should read in binary mode, indicated by `rb` here.

```python codeanim
write('dosbox_data')
tap(Key.enter, modifiers=[Key.shift])
```

If we evaluate the variable, Python gives us a byte view of the data. Each hex value is represented by `\x` followed by two digits.

```python codeanim
write('hl.HexView(dosbox_data)')
tap(Key.enter, modifiers=[Key.ctrl])
```

We can also use Hexly to view the byte data. By default, it assumes ASCII encoding.

```python codeanim
tap(Key.enter)
tap(Key.right, modifiers=[Key.cmd])
tap(Key.left)
write(", encoding=hl.IBM437")
tap(Key.enter, modifiers=[Key.ctrl])
```

We can change the encoding to Code Page 437 by setting the encoding parameter, and if we re-evaluate the cell, we can see our original characters from Dos!

Now, one last demo. Cipherly encodes its payload in the URL using a URL-safe base64 encoding of a MessagePack binary. Let's use Hexly to take a look.

```python codeanim cipherly
chrome.new_tab()
chrome.navigate("https://cipherly.app/password/encrypt/")
tap(Key.tab, repeat=4)
write("test")
tap(Key.tab)
write("test")
tap(Key.tab)
tap(Key.enter)
pause()
tap(Key.tab, repeat=2)
tap(Key.enter)
pause()
chrome.close_tab()
```

So first, let's encode a secret using Cipherly. And then copy the ciphertext.

```python codeanim messagepack
tap("b")
tap(Key.enter)
write("import base64\n")
write('cipherly_data = base64.urlsafe_b64decode("')
tap("v", modifiers=[Key.cmd])
tap("=", repeat=2)
tap(Key.right, repeat=2)
tap(Key.enter)
write("cipherly_data")
tap(Key.enter, modifiers=[Key.shift])
```

Now, back in Jupyter, we can use `base64.urlsafe_b64decode` to decode the ciphertext. Here we can see the Python byte string.

```python codeanim
write("hl.HexView(cipherly_data)")
tap(Key.enter, modifiers=[Key.shift])
```

And here is the hex view of the data using Hexly. Now, we can clearly see, or at least somewhat see, that we have our three fields, salt, initialization vector (iv), and ciphertext in this payload.

If we lookup the MessagePack spec, we'll see that 83 encodes a map of three elements. A4 encodes a string of length 4, which is `salt`. C4 encodes a binary string whose length is 16 bytes (10 in hex). After 16 bytes, we see A2 which encodes a string of length 2, which is `iv`. We see C4 again, encoding a binary string whose length is 12 bytes (0C in hex). After those 12 bytes, we see AA which encodes a string of length 10, which is `ciphertext`. We see C4 a third time, encoding a binary string whose length is 20 (14 in hex). The remaining 20 bytes is the encrypted cipher text.

# Outro

So, to get that demo of WordPerfect working, I used a free tool called DosBox, which emulates a Dos environment on my Mac. I'll admit, that it was really fun strolling down memory lane. If you enjoyed that, hit the thumbs up!

This week, we hit our next milestone. We now have 2^7, or 128 subscribers! The next milestone will be 2^8, or 256 subscribers. Let me know in the comments how you'd like to celebrate the 2^8 milestone!

More videos about Cipherly and other things that pique my interest will be landing in the near future. Subscribe so you don't miss those videos. Thanks for watching, and I'll see you in the next one!
