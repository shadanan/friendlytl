# Vite + Rust + WebAssembly Dev Environment Tutorial

## Introduction

Hello fellow friendos! I'm the Friendly TL.

I have a short tutorial for you today on setting up an environment where you can compile some Rust code to WebAssembly, integrate with TypeScript, and bundle it all together with Vite.

Before we start, ensure that you have Node.js, NPM, and Rust installed. I have these versions installed.

## `wasm-pack`

First, we need to install wasm-pack. This tool is responsible for compiling our Rust code into the WebAssembly binary. So we say:

```sh
cargo install wasm-pack
```

Next, we use wasm-pack to initialize a new project. So we say:

```sh
wasm-pack new vite-rust-wasm
```

Let's open the project in VS code.

```sh
cd vite-rust-wasm
code .
```

If we expand the `src` folder, we can see this `lib.rs` file which is the entry point to our WebAssembly. When we build the WebAssembly, wasm-pack will look for this file.

Inside this file, we see that we are provided with a greet function. Let's modify it to do some string formatting instead of alerting. So we'll have the function take name as an argument. And that's a borrowed string reference. And then we'll return the formatting string, hello, name.

Let's compile the project. So we say:

```sh
wasm-pack build
```

The output of our build is this `pkg` folder.

## Vite

Okay, now let's install Vite. So we say:

```sh
npm init vite .
```

Vite is usually expecting the directory to be empty, but in this case, we already have a wasm-pack project configured. To get Vite to produce its files anyway, let's select option 3 to Ignore files and continue.

Here, we can now select which Framework we want to use. Let's use Svelte with TypeScript.

## Launch

Now that we're done scaffolding, let's do what Vite says to do:

```sh
npm install
npm run dev
```

Let's follow this link. There's our app.

Let's put VS Code and the browser side by side.

## Wire Up WebAssembly

Ok, let's open up App.svelte and remove all of this noise. Next, let's import our greet WebAssembly function from JavaScript. So, we'll say:

```javascript
import { greet } from "../pkg/vite_rust_wasm";
```

Okay, so we have an error, and it helpfully suggest that we use `vite-plugin-wasm`.

The documentation page for this plugin suggests we install `vite-plugin-wasm` and `vite-plugin-top-level-await`. So, let's stop the server, and install those dependencies. Next, let's add the plugins to our list of plugins in `vite.config.ts`.

Next, let's run our dev server again. Great, it's working with our import. Now, let's call our greet function again!

And there is our message from Rust!

## Outro

Thanks for watching this short tutorial. Thumbs if you liked it. Subscribe if you want to see more. I'll see you in the next one!
