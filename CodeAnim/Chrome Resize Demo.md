# Intro

I've made some updates to CodeAnim that enable it to resize windows, and to control and animate Google Chrome. Let's take a look!

# Motivation

CodeAnim is a tool that helps me make recorded video demos. Basically, I write a script in Markdown, and then I read it to the camera. You're watching me read it right now. Interspersed in the script are CodeAnim commands, like this:

```python codeanim
vscode.activate()
vscode.jump(38)
```

These commands will activate the VS Code window, and jump to line 38, which will be useful when I run CodeAnim, you'll see!

The first version of CodeAnim was designed mainly to animate VS Code. However, as I used it, I quickly realized that I need to be able to animate apps other than VS Code, and be able to rearrange windows. So, I've made some updates which I'd like to demo for you now!

# Demo

## Resize

Here you can see that we have a Terminal, a Chrome, and a VS Code window open.

I'll start the demo by calling CodeAnim in this Terminal. The second argument is the script, Chrome Resize Demo.md. I'm setting the verbose flag, `-v` so that we can see the commands that CodeAnim will be evaluating as we go!

For this ScreenCast, I'm recording just a portion of my screen. The top left coordinate is (0, 25), and I'm recording an area that is 1920x1080. So, first, we're gonna position VS Code on the left and have it take up 50% of the recording area. Let's run the CodeAnim script to see it in action!

The first command is the activate command from before, and the scroll command.

```python codeanim
vscode.resize((0, 25), (1920//2, 1080))
```

The next command is the resize command, and it sets the top left position of VS Code to 0, 25, and its width to 1920/2 and its height to 1080.

```python codeanim
chrome.resize((1920//2, 25), (1920//2, 900))
```

Next, we'll resize Chrome. We'll set its top left position to be the midpoint of the recording area, 25, and its width also to 1920/2, and its height to 900, which leaves a bit space for the terminal, which I conveniently resized to fit nicely in this little square before I started the screencast!

## Chrome

```python codeanim
vscode.jump(57)
```

This command scrolls the VS Code window so that you can continue reading what I'm saying. Next, let's demo the new Chrome commands.

```python codeanim
chrome.activate()
chrome.navigate("https://www.github.com/shadanan/codeanim")
```

So, we'll start by activating Chrome. Then, navigate to my GitHub page.

```python codeanim
chrome.toggle_devtools()
chrome.next_devtools_panel(times=2)
chrome.refresh()
```

Next, we'll open the Chrome dev tools. Switch to the Network panel. Refresh the page, and we can observe all the network traffic.

```python codeanim
chrome.prev_devtools_panel(times=2)
write('console.log("Hello from CodeAnim!");\n')
chrome.toggle_devtools()
```

```python codeanim
vscode.activate()
vscode.jump(89) # Just a quick scroll! 📜
chrome.activate()
```

Next, we'll switch back to the Console panel. And we'll run a little JavaScript to have CodeAnim say hello!

```python codeanim
chrome.navigate("https://www.youtube.com/@FriendlyTL")
chrome.back()
chrome.forward()
chrome.new_tab()
chrome.previous_tab()
chrome.close_tab()
```

We've also added a few navigation commands. So for example, we can navigate to my YouTube page, then go back in the history. We also have CodeAnim commands to create a new tab, switch to the previous tabs, and close a tab.

# Outro

CodeAnim is still very much a work in progress. But, if you'd like to use it to automate the recording of one of your video demos, you'll find the relevant links down in the description. If you have questions or feature requests, drop them in the comments! If you liked this video, hit the thumbs up, and if you like this kind of content, click all those other buttons too. Thanks for watching, and I'll see you in the next one!
