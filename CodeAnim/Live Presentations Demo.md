# Intro

Hello. I'm the Friendly TL.

So, my channel has just reached an important milestone. For the first time, I have viewers that are not my family, friends, or peers. And I wanted to talk a little bit about why I started this channel.

So, this is an edutainment channel about software engineering, but I'm also very interested in making apps that people can use. Things like, CodeAnim, which I've been making videos about.

Apps are a little different from other kinds of products and services, because, as an individual, I can write some software, and release it to a limitless number of users. This is in contrast to other things that you might be passionate about, like cooking. You can only make food for few other people.

So, the goal of this channel is to create a community where I can share my knowledge about software engineering, share the software that I make, and engage with my viewers. I actually think there are a lot of people who are a lot like me. People who want to make useful apps and services and make them available on GitHub. The problem is, it's not useful to make cool apps and services if nobody knows about them.

So, I got my first comment from a viewer asking for a new feature in CodeAnim. And this is very exciting for me, because now I know that there is at least one other person interested in using CodeAnim.

Well, I've added the feature – it was actually a very simple ask. Basically, CodeAnim can now open your VS Code project. Here's the demo!

# Demo

```python codeanim
vscode.open("~/open-ws-run-script")
```

So, `vscode.open` is the new command that will open a VS Code folder or workspace. Here, we're going to open a folder called `open-ws-run-script`.

In addition to being able to open projects, CodeAnim can now also be used for live presentations. Basically, after each of these CodeAnim blocks, a `wait()` is inserted which waits for the shift key to be pressed before the animation proceeds.

Okay, let's run the CodeAnim script, and we'll pass the `--live` flag to enable live presentations. So, VS Code opens and then we are prompted to hit shift to proceed.

```python codeanim
vscode.resize((0, 25), (960, 1080))
chrome.resize((960, 25), (960, 900))
vscode.focus("stdemo.py")
```

The next set of commands resize VS Code and Chrome and opens the demo script. This script is a basic Streamlit app that prints out a summary of this demo.

```python codeanim
vscode.focus_terminal()
write("streamlit run stdemo.py\n")
```

Let's hit shift again. Next we focus the terminal, and launch the Streamlit app.

Okay, that's our short CodeAnim demo!

# Outro

This video celebrates my first milestone. But, I'd also like to celebrate future milestones with you. So I'm thinking that we can celebrate a milestone every time my subscriber count crosses a power of two. The next one is 2^7, or 128 subscribers.

Until then, I'll be publishing videos approximately once a week, and we'll see how things go. If you liked this video, hit the thumbs up. And if you'd like to join me on this journey, consider subscribing! See you in the next one!
