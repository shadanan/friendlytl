# Intro

In my last video, I demoed Cipherly, a webapp for sharing secrets. Before releasing that video, I wanted Cipherly available for people to use on the web. The process of setting up my dev environment and productionizing the app was interesting. And I'd like to share it with you!

# Overview

Cipherly is a SvelteKit Single Page App served by a Rust based web framework called Rocket.

There's several cool things about this environment.

When running in dev mode, the Vite frontend dev server proxies API requests to Rocket so that we don't have to deal with Cross Origin Resource Sharing. And auto reload is enabled by default for both Rocket and Vite. This allows us to make changes to both frontend and backend code and immediately test them.

When running in prod mode, Rocket serves the compiled Single Page App from a static folder. We use a multi-stage Dockerfile to build a minimal container that contains just our app. When all's said and done, the final container can be deployed to any serverless container platform, such as Kubernetes, Google Cloud Run, or AWS Fargate.

So, in this tutorial, we're going to build a simplified webapp called Time Getter which gets the time, of course, when you click the Get Time button.

So, here's the roadmap:

1. Initialize Rocket and build a basic `/api/time` endpoint
2. Initialize SvelteKit and build a page that calls the `/api/time` endpoint
3. Configure SvelteKit and Rocket to build for a prod environment
4. Containerize our app using Docker
5. And finally, deploy the app to Google Cloud Run

# Demo

```python codeanim
vscode.activate()
```

So here's a new empty project called `timegetter`.

## Initialize Rocket

We'll start by initializing Rocket.

```python codeanim rocket-init
vscode.toggle_terminal()
write("cargo new backend --name timegetter --vcs none\n")
```

This command creates a new Rust app called timegetter in the backend folder. Setting `--vcs none` skips creating a git repo.

```python codeanim
write("cd backend\n")
write("cargo add rocket --features json\n")
```

Next, we'll add Rocket to our Rust project. And we'll enable support for JSON.

```python codeanim
write("cargo add serde --features derive\n")
```

We'll also add serde with the derive feature so that we can easily convert structs to JSON.

```python codeanim
write("cargo add chrono\n")
```

And we'll add chrono so that we can easily create formatted time strings.

```python codeanim
vscode.toggle_terminal()
vscode.focus("main.rs")
```

Now, let's open up the main file.

```python codeanim
tap("a", modifiers=[Key.cmd])
paste("""#[macro_use]
extern crate rocket;

use rocket::serde::json::Json;
use serde::Serialize;

#[derive(Serialize)]
struct Time {
    time: String,
}

#[get("/time")]
fn time() -> Json<Time> {
    Json(Time {
        time: chrono::Utc::now().to_rfc3339(),
    })
}

#[launch]
fn rocket() -> _ {
    rocket::build().mount("/api", routes![time])
}
""")
vscode.save()
```

And let's replace the contents with the boilerplate for our server. We'll have one route which returns the current time when you do a get at `/api/time`.

This Time struct derives Serialize which enables our API to automatically serialized to JSON. And here, we are using chrono to get the time as a string in RFC3339 format.

```python codeanim
vscode.toggle_terminal()
write("cargo watch -x run\n")
```

Okay. Let's start our new server! The `watch` command will reload the server whenever a file changes.

```python codeanim
chrome.activate()
chrome.navigate("localhost:8000/api/time")
```

Let's verify that our API is returning the current time.

```python codeanim
chrome.refresh()
```

Additionally, if we refresh the page, we can see that our API returns an updated time, and our time changes.

## Initialize SvelteKit

```python codeanim sveltekit-init
vscode.activate()
tap("`", modifiers=[Key.ctrl, Key.shift])
```

Let's leave Rocket running.

```python codeanim
write("npm create svelte@latest frontend\n")
```

And in a new terminal, create a new SvelteKit app in a folder called frontend.

```python codeanim
tap(Key.down)
pause()
tap(Key.enter)
```

Let's select a Skeleton project.

```python codeanim
tap(Key.down)
pause()
tap(Key.enter)
```

Yes to using Typescript.

```python codeanim
tap(Key.enter)
```

And no additional options.

```python codeanim install-sveltekit
write("cd frontend\n")
write("npm install\n")
```

Next, let's install the dependencies.

```python codeanim run-sveltekit
write("npm run dev\n")
```

Start the SvelteKit dev server.

```python codeanim chrome-open-spa
chrome.activate()
chrome.navigate("localhost:5173")
```

And open it up in the browser.

```python codeanim
vscode.activate()
vscode.toggle_terminal()
vscode.focus("+page.svelte")
```

Okay, now we need to build our Time Getter SvelteKit app. We'll start by opening up the main page.

```python codeanim
tap("a", modifiers=[Key.cmd])
paste("""<script lang="ts">
  let time: Promise<Time> | null = null;

  type Time = {
    time: string;
  };

  async function fetchTime(): Promise<Time> {
    const response = await fetch("/api/time");
    const result = await response.json();
    return result;
  }
</script>

<h1>Time Getter</h1>

<button on:click={() => (time = fetchTime())}>Get Time</button>

{#if time}
  {#await time}
    <div>Fetching time...</div>
  {:then time}
    <div>Current time: {time.time}</div>
  {:catch err}
    <div>Failed to fetch time: {err}</div>
  {/await}
{/if}
""")
vscode.save()
```

And replace it with our Time Getter frontend code.

This is the Typescript type for the Time response from our API. It corresponds to the Time struct from Rocket.

Here we have our fetchTime function. This calls our endpoint and returns the response as a Time object.

Here we have our Get Time button. When clicked, it will invoke our fetchTime function and assign the response to the time variable.

Finally, at the bottom, we have our template. If time is not null, then it will be a promise. If the promise hasn't resolved, we print "Fetching time...". If it has resolved, we print the current time. And if it failed, we print an error.

```python codeanim
vscode.toggle_terminal()
chrome.activate()
tap(Key.tab)
tap(Key.enter)
```

Let's click the Get Time button.

Okay, there's an error. A hint at the problem is here: the `/api/time` endpoint is not found. The problem is that our API endpoint exists on the Rocket backend server, but we are calling `/api/time` on the Vite frontend server.

We can fix this by configuring Vite to proxy requests to Rocket for us.

```python codeanim configure-proxy
vscode.activate()
vscode.focus("vite.config.ts")
```

Let's open the Vite frontend dev server config.

```python codeanim
vscode.jump(5, 27)
paste(""",
  server: {
    proxy: {
      "/api": {
        target: "http://localhost:8000",
        changeOrigin: true,
        secure: false,
      },
    },
  },""")
vscode.save()
```

And we'll add this proxy code. Basically, we are proxying all calls destined for `/api` to our Rocket backend server on port 8000.

```python codeanim
chrome.activate()
tap(Key.tab)
tap(Key.enter)
```

That should do it. Let's click the Get Time button again.

There's the time! Excellent!

Note, that we didn't have to proxy requests. We could have fetched directly to Rocket's host-port, but this leads to Cross Origin Resource Sharing errors. I find that proxying is a more elegant solution as it mirrors how the app works in Prod.

```python codeanim shutdown-servers
vscode.activate()
tap("k", modifiers=[Key.cmd])
tap("w", modifiers=[Key.cmd])
vscode.toggle_terminal()
tap("c", modifiers=[Key.ctrl])
pause()
tap("d", modifiers=[Key.ctrl])
pause()
tap("c", modifiers=[Key.ctrl])
pause()
tap("d", modifiers=[Key.ctrl])
pause()
```

## Configure Prod Build

By default, SvelteKit assumes that a Node.js server is running to provide Server Side Rendering. However, that's not the case for us. In our Time Getter project, we are using our own Rocket server. So, we need to configure SvelteKit to render a Single Page App instead.

```python codeanim configure-spa
vscode.toggle_terminal()
write("cd frontend\n")
write("npm install --save-dev @sveltejs/adapter-static\n")
```

The first step is to install the static adapter.

```python codeanim
vscode.focus("svelte.config.js")
vscode.jump(1, 44)
backspace(4)
write("static")
vscode.save()
```

Next, let's configure SvelteKit to use the static adapter. So, we open `svelte.config.js` and just change `auto` to `static`.

```python codeanim
vscode.new_file()
paste("""export const prerender = true;
export const ssr = false;
export const trailingSlash = "always";
""")
```

Now, we need to configure SvelteKit's behavior. These magic values configure SvelteKit to operate as a Single Page App.

```python codeanim
tap("s", modifiers=[Key.cmd])
pause()
tap("g", modifiers=[Key.cmd, Key.shift])
pause()
write("src/routes\n")
pause()
write("+layout")
pause()
tap(Key.enter)
```

Let's save that file into `src/routes/+layout.ts`.

```python codeanim spa-build
vscode.toggle_terminal()
write("npm run build\n")
```

Finally, we can run `npm run build` and we should get our Single Page App.

And there it is in the build folder!

Next, we need to configure Rocket to serve our Single Page App.

```python codeanim prod-rocket
tap("d", modifiers=[Key.ctrl])
pause()
vscode.focus("main.rs")
```

So, let's re-open `main.rs`.

```python codeanim rocket-static
vscode.jump(4)
vscode.newline(above=True)
write("use rocket::fs::FileServer;")
```

And we'll use rocket's built-in FileServer.

```python codeanim
vscode.jump(22, 49)
write('\n.mount("/", FileServer::from("./static"))')
vscode.save()
```

Then, we'll mount the folder called `static` into the root path. Note that this folder doesn't exist yet. We'll create in a moment.

Now, with this configuration, if the route does not match `/api/time`, then Rocket will attempt to serve static content. If no content exists at that path, Rocket will return a 404 not found error.

There's one last thing to do in `main.rs`. When we deploy, Google Cloud Run will configure a port using the environment variable `PORT`. However, Rocket's port is configured via the `ROCKET_PORT` environment variable.

```python codeanim
vscode.jump(22)
vscode.newline(above=True)
write('env::set_var("ROCKET_PORT", env::var("PORT").unwrap_or("8000".into()));')
vscode.jump(4)
vscode.newline(above=True)
write('use std::env;')
vscode.save()
```

As a quick hack, we can just copy the `PORT` environment variable into the `ROCKET_PORT` environment variable before we call `rocket::build()`.

```python codeanim static-symlink
vscode.toggle_terminal()
write("cd backend\n")
write("ln -s ../frontend/build static\n")
```

Now, let's create a symlink called `static` that points to the built frontend in `frontend/build`.

```python codeanim launch-rocket
write("cargo run\n")
chrome.activate()
chrome.navigate("localhost:8000")
```

Finally, let's launch Rocket and navigate to port 8000. There's our Time Getter being served by Rocket instead of the dev server.

```python codeanim
tap(Key.tab)
tap(Key.enter)
```

Click on Get Time.

And, there's the current time! Excellent!

```python codeanim
vscode.activate()
tap("c", modifiers=[Key.ctrl])
pause()
tap("d", modifiers=[Key.ctrl])
pause()
tap("k", modifiers=[Key.cmd])
tap("w", modifiers=[Key.cmd])
```

## Dockerize

To get Rocket and our Single Page App running on Google Cloud Run, we need to put everything into a Docker container.

```python codeanim dockerfile-create
tap("e", modifiers=[Key.cmd, Key.shift])
vscode.new_file()
tap("s", modifiers=[Key.cmd])
pause()
tap(Key.up, modifiers=[Key.cmd], repeat=2)
write("Dockerfile")
tap(Key.enter)
```

So, let's create a new file and save it as `Dockerfile` at the root of our project.

In this Dockerfile, we will have three stages. In the first stage, we will build the Rocket binary. In the second stage, we will build the SvelteKit Single Page App. And in the last stage we will create a minimal image and copy the important artifacts from the previous stages.

```python codeanim dockerfile-rust
write("""FROM rust AS rust

WORKDIR /app

COPY backend/Cargo.toml backend/Cargo.lock ./
COPY backend/src ./src

RUN cargo build --release

""")
vscode.save()
```

Okay. So, in the first stage, we will build our Rocket binary. We start by using the `rust` Docker image. Then, we set our working directory to `/app`. Then we copy our Cargo files and our `src` folder to the stage. And finally we run the `cargo build --release` command.

```python codeanim
vscode.toggle_terminal()
write("docker build -t gcr.io/cipherly/timegetter .\n")
```

We can build the stage and inspect it. Let's run the docker build command.

```python codeanim
write("docker run -it gcr.io/cipherly/timegetter ls -al\n")
```

And then let's run the `ls` command and we can see that the files we copied are there.

```python codeanim
write("docker run -it gcr.io/cipherly/timegetter ls -al /app/target/release\n")
```

And our `timegetter` binary should be located in `/app/target/release`.

There it is! On to the second stage.

```python codeanim
vscode.toggle_terminal()
write("""FROM node AS node

WORKDIR /app

COPY frontend/*.json frontend/*.js frontend/*.ts ./
RUN npm install

""")
vscode.save()
```

In this stage, we use the `node` Docker image. Then we set our working directory, and copy our frontend config files, such as `package.json` to the stage. Then we run `npm install` to install the `node_modules`.

```python codeanim
write("""COPY frontend/src ./src
COPY frontend/static ./static
RUN npm run build

""")
vscode.save()
```

Next, we copy the source code and any static files to the stage. And then build our app.

```python codeanim
vscode.toggle_terminal()
write("docker build -t gcr.io/cipherly/timegetter .\n")
```

Let's build the stage and inspect it again. Let's run the docker build command.

```python codeanim
write("docker run -it gcr.io/cipherly/timegetter ls -al\n")
```

This time when we run the `ls` command, we're looking at the files in the second stage. And we should see our `build` directory.

There it is! Now for the final stage.

```python codeanim
vscode.toggle_terminal()
write("""FROM gcr.io/distroless/cc-debian12

WORKDIR /app

COPY --from=rust /app/target/release/timegetter ./
COPY --from=node /app/build ./static

ENV PORT=8000
ENV ROCKET_ADDRESS=0.0.0.0

CMD ["./timegetter"]
""")
vscode.save()
```

So, in the final stage, we are going to use `distroless/cc-debian12` as the base image. This provides the libc dependencies for our Rust binary. Then, set the working directory. And now the interesting part. We copy the `timegetter` binary from the `rust` image, and we copy the `build` folder from the `node` image. Then we configure the port and bind address for Rocket, and then invoke our timegetter binary.

```python codeanim
vscode.toggle_terminal()
write("docker build -t gcr.io/cipherly/timegetter .\n")
```

Okay, let's test it out! So first, let's build the Docker image.

```python codeanim
write("docker run -p8000:8000 gcr.io/cipherly/timegetter\n")
```

And then run it, forwarding port 8000.

```python codeanim
chrome.activate()
chrome.navigate("localhost:8000")
```

Let's navigate to it. And there's our Time Getter app running from our productionized container!

```python codeanim
tap(Key.tab)
tap(Key.enter)
```

Click the Get Time button.

There's the time! Excellent!

```python codeanim
vscode.activate()
tap("c", modifiers=[Key.ctrl])
vscode.toggle_primary_sidebar()
```

## Deploy

Alright, let's launch TimeGetter to Google Cloud Run! There are a few prerequisites.

First, you'll need to create a project on Google Cloud. And then you'll need to install the gcloud command, authorize it, and activate your project.

```python codeanim gcr-submit
write("gcloud builds submit --tag gcr.io/cipherly/timegetter\n")
```

Once you're done with those prerequisites, the next step is to run the gcloud command to submit our Docker image to Google Container Registry. This part takes a minute.

```python codeanim gcr-deploy
write(r"""gcloud run deploy timegetter \
  --image gcr.io/cipherly/timegetter \
  --region us-west1 \
  --allow-unauthenticated
""")
```

Next, we run the gcloud deploy command, passing our `timegetter` docker image. When this command completes, we get a service URL.

```python codeanim prod-navigate
chrome.activate()
chrome.navigate("https://timegetter-d7q5lnxuua-uw.a.run.app")
tap(Key.tab)
tap(Key.enter)
```

If we navigate to that URL, we see that our Time Getter app is live!

# Outro

Alright, so that was my tutorial on building and deploying a Rust Rocket SvelteKit Singe Page App to Google Cloud Run. Now that's a mouthful! Source code for Time Getter is available on GitHub. You can find the links in the description.

If you have topics you'd like me to cover, drop them in the comments. I'd love to engage with you. This tutorial was requested by my editor. Thumbs if you liked it, and subscribe if you want to see more. Thanks for watching, and I'll see you in the next one.
