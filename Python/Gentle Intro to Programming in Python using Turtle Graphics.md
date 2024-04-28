# Intro

Friends and family frequently ask me how to learn to code. And I would tell them that the best way to learn is to build something. The problem is, the things that most people want to build are not easy to code. As a mentor, I have to guide my student to ideas that are both interesting and easy enough to do.

This videos is the first in a series where we will use Python to make some art using turtle graphics. By the end of the series, we'll have made this animation.

This video is specifically for my nephew who is just starting to learn to code. But it's appropriate for anyone who would like a gentle introduction to programming. Python is a very beginner friendly language, and making pretty art is fun.

# Prerequisites

Before we start, we need to install Python and a code editor. For my nephew, who is using a Raspberry Pi, I've already installed these things for you, so you can skip to the next chapter.

```python codeanim download-python
chrome.activate()
chrome.navigate("https://python.org/downloads/")
```

For everyone else, you can download Python from https://python.org/downloads/.

```python codeanim download-vscode
chrome.new_tab()
chrome.navigate("https://code.visualstudio.com/")
```

We're also going to need a code editor. You can download VS Code from https://code.visualstudio.com/.

```python codeanim config-vscode
vscode.activate()
click((38, 462))
write("Python")
click((368, 315))
```

Once installed open up VS Code, then open the extensions panel by clicking this button. Then, search for Python in this search box. And then, install the Python extension by clicking this install button.

```python codeanim
click((38, 545))
click((350, 117))
```

Okay, now that we've got everything installed, let's close these things and start writing some code!

# Turtle Graphics

Our goal for this video is to draw a square like this. I suggest that you watch the video once through first. Then watch the video a second time, pausing as needed, so that you can try it yourself.

```python codeanim create-new-file
move((350, 117))
vscode.activate()
click((117, 17))
click((190, 66))
click((430, 200))
```

The first step is to create a new file. We can do this by clicking the File menu, New File, Python File.

```python codeanim save-file
click((117, 17))
click((155, 297))
write("art")
click((640, 640))
```

Let's save our file. Click File, Save. Then type art, and click Save.

```python codeanim import
write("import turtle\n\n")
write("annie = turtle.Turtle()\n\n")
write("turtle.done()\n")
vscode.save()
```

Next, we'll import the turtle module. Then we type, `annie = turtle.Turtle()`. This creates a friendly turtle named Annie. Notice that this T is a capital T. Finally, we type `turtle.done()`.

```python codeanim run-1
click((809, 122))
move((759, 122))
```

Let's run our program! To do that, click the triangle play button here. This triangle is our turtle named Annie, and as we can see, Annie is facing right.

```python codeanim forwards
vscode.activate()
vscode.jump(4)
write("annie.forwards(100)\n")
```

Let's make Annie move forward. So, after we create our turtle named Annie, we type `annie.forwards(100)`. This will make Annie move forward by a hundred.

```python codeanim run-2
click((974, 41))
click((809, 122))
move((759, 122))
```

Now, before we can run our program, we have to first close the previous program. So, click the "x" button to close the window. Now we can click the triangle play button again to run our program.

Uh, oh, what's this? This is an error message. I know that it looks scary, but it's not. You just have to know where to look. If we look down, it says:

```
AttributeError: 'Turtle' object has no attribute 'forwards'. Did you mean: 'forward'?
```

```python codeanim
click((373, 292))
backspace()
tap(Key.down)
click((809, 122))
move((759, 122))
```

Ah, we made a mistake. But Python helpfully points out that we made a typo right here. Let's remove that extra `s` and rerun our program by clicking the triangle play button again. And this time, Annie moves forwards! Great!

```python codeanim turn-1
vscode.activate()
write("annie.right(90)\n")
```

To get Annie to draw a square, we need to turn Annie by 90 degrees. So after moving forwards, we type, `annie.right(90)`. This will make Annie turn to the right by 90 degrees.

```python codeanim run-2
click((974, 41))
click((809, 122))
move((759, 122))
```

Let's close the turtle graphics window, and run our program again. Now we see that Annie is facing down! That's exactly what we want.

```python codeanim square
vscode.activate()
write("annie.forward(100)\n")
click((974, 41))
click((809, 122))
move((759, 122))
```

Now, to draw the right side of the square, we just need to move Annie forwards another hundred units. So we type, `annie.forward(100)`. Restart the program, and Annie now draws both the top, and right side of our square.

```python codeanim finish-square
vscode.activate()
write("annie.right(90)\n")
write("annie.forward(100)\n")
write("annie.right(90)\n")
write("annie.forward(100)\n")
click((974, 41))
click((809, 122))
move((759, 122))
```

To finish the square, we just need to turn right again and move forwards by a hundred. This draws the bottom of the square. Turn right one last time and move forwards. This draws the left side of the square. Restart the program and Annie now draws the entire square.

```python codeanim comments
vscode.activate()
click((423, 292))
write("  # Top of square")
```

Let's add some comments to our code so that it's easier to understand what the various commands are doing. The first forward command to Annie draws the top of the square. So we can add the comment "Top of square".

```python codeanim
click((423, 354))
write("  # Right side of square")
click((423, 416))
write("  # Bottom of square")
click((423, 478))
write("  # Left side of square")
click((974, 41))
click((809, 122))
move((759, 122))
```

The second forward command draws the right side of the square. The next one draws the bottom, and the last draws the left side. Let's rerun our program one last time to make sure everything still works. That's a nice looking square that our turtle drew.

# Outro

How would you make an octagon? How about a hexagon? Give it some thought, and maybe try it yourself. I've linked the turtle graphics documentation page in the description. There are so many fun things that you can do. Maybe try adding some color to start turning those lines into some art!

This video is the first in a series that gently introduces people to programming using Python and the turtle graphics module.

If you liked this video, hit the thumbs up. I'm The FriendlyTL and I make edutainment videos about software and open source apps that I also make. If you're interested in this kind of content, consider subscribing. Thanks for watching; I'll see you in the next one!
