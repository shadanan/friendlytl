```python codeanim header
def rerun():
    click((974, 40))
    click((830, 102))
    wait()
```

# Intro

In our last video, we had our three turtles, Annie, Anvi, Dima take turns to draw some cool shapes. Annie started first drawing an orange square, followed by Anvi that drew a green hexagon around Anvi's square, and finally Dima that drew a octagon around Anvi's hexagon.

But did you notice that when we were writing the code to draw these shapes we wrote the same lines over and over again. That can get a bit repetitive and boring, right? Well, guess what? There's a special way in Python called a `for` loop that can helps us avoid repeating ourselves!

Today, we are going discover how to use a `for` loop to make our coding life much easier and fun!

# `for` loop

This is the code we wrote last time. Let's reuse this code to write a `for` loop.

```python codeanim new-file
vscode.activate()
vscode. resize((0, 25), (1920//2, 1080))
tap("a", modifiers=[Key.cmd])
tap("c", modifiers=[Key.cmd])
tap("n", modifiers=[Key.cmd])
tap("v", modifiers=[Key.cmd])
tap("s", modifiers=[Key.cmd])
write('loops')
click((645, 645))
click((830, 102))
```

So first, let's select this code, you can select all the code by pressing Ctrl+A or Cmd+A if you're on a Mac. Then click Ctrl+C to copy, or Cmd+C on a Mac.

Now, let's create a new file. You can Click File, New File or press Ctrl+N or Cmd+N if you're on a Mac.

Paste our previous code pressing Ctrl+V or Cmd+V if you're on a Mac.

And let's save it. File, Save or press Ctrl+S or Cmd+S if you're on a Mac. And we'll name it `loops.py`. Save. Let's make sure that it runs. Click the triangle. And there are our shapes from last time!

```python codeanim square
vscode.activate()
vscode.jump(11)
drag((113, 303), (410, 414))
write("\b")
write('for side in range(4):\n')
write('annie.forward(100)\n')
write('annie.right(90)\n')
rerun()
```

Now, let's have Annie draw a square again, but smarter this time! To do this, we first select and delete this code. Then we type `for side in range(4):` then, new line. Notice that the new line brings us inside the for loop. Then type `anvi.forward(150)` and `anvi.right(60)`. Close and run. Amazing!

In Python, we use a `for` loop to repeat an action multiple times but with fewer lines of code. `range()` tells the computer how many times to repeat something. So `range(4)` repeats the loop 4 times, which is perfect for drawing a square with 4 sides.

`side` is a counter that keeps track of how many sides of the shape we've already drawn. Each time the loop runs, `side` represents the next side of the shape we're going to draw.

Notice, the two lines of code are inside the for loop. We do this to tell Python which code belong to the loop. This way only the code inside the `for` loop will be repeated.

So, basically this for loop tells the computer "Keep doing these steps in order until you have made all 4 sides of the square".

```python codeanim hexagon
vscode.activate()
vscode.jump(24)
drag((116, 546), (215, 738))
write("\b")
write('for side in range(6):\n')
write('anvi.forward(150)\n')
write('anvi.right(60)\n')
rerun()
```

Great! now that you know the trick, pause the video and try it yourself with Anvi and Dima!

Same steps again, we select and delete the code. Then we type `for side in range(8)` then new line, then we `anvi.forward(150)` followed by `anvi.right60)`. Close and rerun. Great!

```python codeanim octagon
vscode.activate()
vscode.jump(37)
drag((114, 549), (208, 823))
write("\b")
write('for side in range(8):\n')
write('dima.forward(200)\n')
write('dima.left(45)\n')
rerun()
```

Dima's turn now! Again, we select and delete the previous code, then we type `for side in range(8)` then new line then `dima.forward(200)` followed by `dima.right(45)`. Close and rerun.

Notice that our code is much smaller and simpler. With a `for` loop, it's just a couple of lines of code, no matter how many times we need to repeat the action. Always remember, smart coders are lazy coders, they make the computer do the hard work!

# Drawing a Spiral

```python codeanim spiral
vscode.activate()
vscode.jump(36)
write('\n')
write('distance = 200')
click((258, 607), count=2)
write('distance')
click((238, 623))
write('\n')
write('distance = distance + 10')
rerun()
```

Now, let's get creative using a `for` loop. Instead of having Dima draw a hexagon, we can have him draw a spiral that goes around Annie's square and Anvi's hexagon.

To draw a spiral shape, Dima has to move a little further each time it moves forward. To do this, we can set Dima's starting distance to be 100 outside of the `for` loop. Then we change the `200` to be the distance, then inside the loop we type `distance = distance + 10`, this way Dima's increases his step by 10 each time he is getting ready to draw and move forward. Close and rerun. This is cool, isn't it?

```python codeanim bigger-spiral
vscode.activate()
click((252, 590), count=2)
write('24')
rerun()
```

We can also make the spiral twice bigger and have Dima go 3 times around or as much as you want you want him to. We only have to change the `range(8)` from 8, to be equal to`8*3` which is `24`. So we type `24`. Close and rerun. Great!

# Outro

Today we learned how to use a `for` loop to make our coding much simpler and to avoid repetition.

You should now be able to make the most beautiful art. I'm curious to know what you end up making! Post your ideas in the comments!

This video is the third in a series that gently introduces people to programming using Python and the turtle graphics module.

If you liked this video, hit the thumbs up. I'm The FriendlyTL and I make edutainment videos about software and open source apps that I also make. If you're interested in this kind of content, consider subscribing. Thanks for watching; I'll see you in the next one!
