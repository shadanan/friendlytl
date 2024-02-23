# Compressing a File in a Browser using WebAssembly

## Introduction

Hello, I'm the friendly TL.

I recently had an idea for a cool new project. A part of this project involves manipulating binary data in a web browser, and I don't really know how difficult this is. So, to figure out if this is possible, I need to build a proof of concept.

## Overview

The proof of concept is straightforward: I want to get a web browser to compress a file without sending the file over the Internet. Let's expand a little on that last part. Here's a Streamlit app that demonstrates what I'm trying to avoid.

1. This Streamlit app is running on the Internet at zipdemo.streamlit.app
1. I have this text file that I want to compress. It contains the text "Hello, World!".
1. Let's upload it to the Streamlit app.
1. The Streamlit app compresses it.
1. And I can click this button to download the compressed file.
1. If I double click the downloaded file, it will decompress, and I can see my original file.

By the way, if you're interested in a tutorial about how I made this demo, drop a comment below.

Now the problem with this demo is that the browser is not compressing the file – the web server is. When I upload the file in my browser, the browser sends the file over the Internet to the Streamlit server, and some Python code on the server compresses the file, and returns it to the browser, where I can then download the file.

In order to demonstrate my proof of concept, we need to eliminate the Streamlit backend, and have the browser itself compress the file and return it.

## Solution

So, the high level idea for the proof of concept is to make a web app that compresses the file using a WebAssembly binary that runs entirely in the browser. We will still need a web server to serve the app, but critically, when you compress a file, it gets compressed by this WebAssembly binary running in the browser, without ever sending the file over the Internet.

## Tech Stack

I did some preliminary research, and there appears to be good support in the Rust programming language for WebAssembly. There is also a relatively mature library, called flate2 for compressing data. I can build a basic frontend using Svelte, and I'll use Vite to bundle and serve the frontend and the WebAssembly binary, and we'll see if we can get the proof of concept working!

## Outro

Links to the GitHub repo where I'm prototyping can be found in the description. I'm the friendly TL. If you liked this content, hit the thumbs up. If you want to see more videos like this, consider subscribing. I'll see you in the next one!
