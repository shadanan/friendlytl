Hello, I'm the Friendly TL.

So, in the last video, I talked about building a proof of concept that would compress a file directly in the browser without sending the file over the internet.

I managed to get the proof of concept working, and for demo day, I'd like to prove to you that my proof of concept works!

So, here is the Streamlit app from the last video. To demonstrate that our uploaded file goes over the internet, we can use Chrome's built-in developer tools. The shortcut to open the tool on MacOS is Command+Option+I.

Once open, we can click on the Network tab.

If we refresh the page, we'll see a bunch of activity. Each row here is a separate request made to the server.

Let's clear the current view by clicking this button. And now, let's get a file compressed. So we click Browse files, select hello.txt, then click Open.

The very first request made here happens to be our file being sent to the server. To prove this, we can click the request, and then we see information about the request here. In the Payload tab, we can see that hello.txt was sent. It's contents are not displayed but is indicated by the word binary here, so our file was indeed sent to the server. Interestingly enough, it was sent before we even clicked the Download button!

Now, I've conveniently placed my proof of concept in a separate tab here. Let's compress a file! So, we click the Choose File button, select hello.txt, then click Open. Notice, no network requests so far!

Now, let's click the Download button, and then click Save. Again, no network requests.

Let's double click the file to decompress it, and preview. There's our Hello, World! All with no network requests!

So how does it work?

```python codeanim
set_delays(tap=0.05, end=2)
focus("lib.rs")
```

Well, the actual code for compressing is written in Rust and as you can see is pretty straightforward. First we define the compress function. It takes an array of bytes, and returns a vector of bytes or an error.

Then we create a Gzip encoder, write all of the passed in data to the encoder, finalize it, and return the compressed data.

Lastly, we annotate our compress function with wasm_bindgen to tell the compiler that we will be using this function from JavaScript.

```python codeanim
focus("App.svelte")
```

Now, let's take a look at the UI code. Unfortunately, this code is complex only because reading the file data from JavaScript and initiating a download from JavaScript are somewhat involved, but I've wrapped that logic in these functions so that we can just invoke them.

```python codeanim
jump(35)
```

At the top, we import our compress function from the WebAssembly binary, then down here we have our compress_and_download function that takes the data, compresses it, and then initiates the download.

```python codeanim
jump(49)
```

Finally, we have our HTML. There is one component for uploading the file. When that component changes, we invoke the read function. Then we have our Download button. It is disabled if no data has been read. Once data exists, and the button is clicked, we invoke our compress_and_download() function.

So, as it turns out, the hardest parts of this proof of concept was setting up my development environment, and figuring out how to use JavaScript to read file data, and trigger downloads. Links to the GitHub repos are in the description.

I have two videos coming up. The first one describes why I needed this proof of concept. Hint, we're going to be doing some cryptography! The second one will just walk through what I had to do to set up my development environment.

If you liked this content, hit the thumbs up. If you're interested in those follow up videos, subscribe! I'm the friendly TL. Thanks for watching!
