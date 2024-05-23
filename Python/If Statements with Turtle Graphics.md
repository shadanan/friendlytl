# Links:

- Turtle Graphics Documentation: https://docs.python.org/3/library/turtle.html#turtle.speed
- Color table: https://shad.io/tkcolors/

```python codeanim header
def run():
    click((830, 102))
    wait()
def rerun():
    with delay(0):
        click((974, 40))
        click((830, 102))
    wait()
def copy():
    click((165, 12))
    click((220, 118))
def paste():
    click((165, 12))
    click((220, 142))
```

# Intro

In our last video, we learned how to simplify repetitive tasks in our code using for-loops. As a result, Keith was able to draw a giant spiral with just a few lines of code, all thanks to the awesomeness of for-loops!

So far, our turtles have simply followed directions. They never made decisions. In this episode, we're going to learn about `if` statements. `if` statements enable our turtles to make decisions! Let's get started!

# If statement

```python codeanim new-file
vscode.activate()
run()
```

This is the code we wrote last time. Let's run it again to make sure everything is working correctly. The spiral is quite impressive, isn’t it?

```python codeanim if-distance
vscode.activate()
vscode.jump(11)
vscode.newline(above=True)
write('if distance > 100:\n')
chrome.activate()
chrome.navigate("https://shad.io/tkcolors/")
tap(Key.space, repeat=2)
vscode.activate()
write('keith.color("CornflowerBlue")')
rerun()
```

Okay, let's have Keith make a decision. Let's say that we want Keith to change his color to blue if he starts traveling very far.

Here, we type `if distance > 100:`. Now let's set Keith's color. I created this color table for you at shad.io/tkcolors/. You can pick any color from this table, and use it as the color name in turtle graphics. This `CornflowerBlue` is nice. So, switch back to VS code and type `keith.color("CornflowerBlue")`. Let's run that.

Noice! Our `if` statement is working!

# if-else Statements: More Decisions!

Alright. Keith has done a great job with loops. We have a new turtle who wants to draw some nice pictures. Her name is Madame Sue!

```python codeanim clear
vscode.activate()
vscode.jump(3)
tap(Key.down, modifiers=[Key.cmd, Key.shift])
tap(Key.up, repeat=2, modifiers=[Key.shift])
tap(Key.left, modifiers=[Key.shift])
tap(Key.backspace)
```

Let's say farewell to Keith and his code. But don’t worry – you'll find a link to his code in the description. Bye Keith!

Now, Madame Sue plans to draw a beautiful flower. Let's help her figure out how to create her colorful masterpiece!

```python codeanim madame-sue
chrome.activate()
vscode.activate()
write('turtle.bgcolor("LightSkyBlue")\n\n')
write('madame_sue = turtle.Turtle()\n')
write('madame_sue.shape("turtle")\n')
write('madame_sue.width(6)\n')
chrome.activate()
vscode.activate()
write('madame_sue.color("DeepPink")\n')
rerun()
```

Let's start by painting our canvas a nice sky blue. This `LightSkyBlue` looks good.

Then, we create our artist turtle, Madame Sue: `madame_sue = turtle.Turtle()`. And of course, she must be the shape of a turtle. Set the width of her line to 6.

Now, let's pick a beautiful color for Madame Sue. I'm gonna go with this Deep Pink but feel free to pick any color that you think Madame Sue will like!

Nice. There's our beautiful sky, and Madame Sue looks ready to start!

```python codeanim grass-1
vscode.activate()
write('\nfor i in range(50):\n')
write('madame_sue.forward(100)\n')
write('if i % 2 == 0:\n')
write('madame_sue.right(170)\n')
write('\belse:\n')
write('madame_sue.left(170)\n')
rerun()
```

Let's try to draw a flower! When Keith made a spiral, we used a for-loop to get him to go around in a circle. That's a good starting place. So, type `for i in range(50):`

Next let's have Madame Sue move forward by let's say 100 units. Type `madame_sue.forward(100)`. Now, let's have alternate between turning left and right. So, type `if i % 2 == 0:`, new line, `madame_sue.right(170)`, new line, `else:`, new line, `madame_sue.left(170)`.

Let's give it a try! Oh, this is interesting. We have a zigzag! So, half the time, we turn 170 degrees to the right, and the other half of the time, we turn back 170 degrees to the left. You know, this zigzag kinda of looks like grass. Actually, having some grass would be nice!

```python codeanim grass-2
vscode.activate()
vscode.jump(10)
vscode.newline(above=True)
write('madame_sue.setheading(85)\n')
write('madame_sue.penup()\n')
write('madame_sue.goto(-500, -520)\n')
write('madame_sue.pendown()\n')
rerun()
```

Let's change Madame Sue's drawing direction to have the grass peaks face upward, and position it at the bottom of the screen. According to the documentation, 0 is east, 90 is north, 180 is west, 270 is south. Let's have Madame Sue start her first move slightly northeast, say by 85 degrees. So, we type `madame_sue.setheading(85)`. Then we move Madame Sue to the bottom left of the screen with `madame_sue.penup()`, `madame_sue.goto(-500, -520)`, and `madame_sue.pendown()`.

```python codeanim grass-3
vscode.activate()
write('madame_sue.color("DarkGreen")\n')
click((330, 552), count=2)
write('120')
tap(Key.up, repeat=7)
write('madame_sue.speed(0)\n')
rerun()
```

Ok, now we have some pink grass. And we kinda stopped halfway. Let's fix it! So first, we change the color to dark green. Now, to get the grass to span the whole bottom of our canvas, we can increase the number of loop iterations, say to 120. Before we rerun, let's get Madame Sue to draw as fast as possible. On line 9, type `madame_sue.speed(0)`.

```python codeanim grass-4
vscode.activate()
tap(Key.down, repeat=6)
write('madame_sue.begin_fill()')
tap(Key.down, repeat=7)
write('madame_sue.end_fill()')
rerun()
```

That's looking great! But we can sorta see the sky behind the grass. We can fix this by filling. Type `madame_sue.begin_fill()` before the loop. Then, when the loop is done, type `madame_sue.end_fill()`.

```python codeanim sun-1
vscode.activate()
drag((165, 584), (165, 740))
copy()
click((165, 404))
vscode.newline()
paste()
click((335, 428), count=2)
write('50')
click((439, 506), count=2)
write('180')
click((429, 558), count=2)
write('160')
rerun()
```

Great. The grass is done! But we got distracted. Madame Sue was trying to draw a flower! Let's give that another try. Let's copy our grass code and try to get it to make a flower. First, let's change our loop back to 50. Now, let's try some different angles to see what happens. When we turn right, let's turn by 180 degrees. And when we turn left, let's turn by 160.

```python codeanim sun-2
vscode.activate()
click((165, 404))
vscode.newline()
write('madame_sue.color("Yellow")\n')
write('madame_sue.penup()\n')
write('madame_sue.goto(350, 400)\n')
write('madame_sue.pendown()')
rerun()
```

Well, it's starting to look like a flower. But you know, right now, it looks more like a sun than anything. Are you thinking what I'm thinking? Let's go! Let's change the color to yellow by typing `madame_sue.color("Yellow")`. And, let's put the sun in the top right corner. Type, `madame_sue.penup()`, `madame_sue.goto(350, 400)`, then `madame_sue.pendown()`.

```python codeanim sun-3
vscode.activate()
click((418, 558), count=2)
write('60')
rerun()
```

The sun's rays are a bit long. We make it smaller by moving forward by 60 instead of a 100. Nice. This gives the illusion that the sun is far away!

```python codeanim flower-1
vscode.activate()
drag((165, 532), (165, 688))
copy()
click((165, 404))
vscode.newline()
paste()
click((440, 506), count=2)
write('170')
rerun()
```

Alright, we set out to draw a flower, and we got grass and a sun. Third time's a charm. This time, for sure, we're gonna make a flower. Let's copy paste our sun code. And this time, let's try changing `180` to `170`.

```python codeanim flower-2
click((330, 428), count=2)
write('80')
rerun()
```

Okay, that's really starting to look like a flower! But Madame Sue stopped shy of completing it. Let's increase the range from `50` to `80`.

```python codeanim flower-3
click((165, 404))
write('\nmadame_sue.begin_fill()')
click((165, 610))
write('madame_sue.end_fill()\n')
rerun()
```

The flower is showing the blue sky behind it. Let's fill it in like we did with the grass. Before the loop, we type `madame_sue.begin_fill()`, then, after the loop, type `madame_sue.end_fill()`.

```python codeanim flower-4
click((330, 454), count=2)
write('70')
rerun()
```

It's almost perfect. But the fill didn't quite work, you can see a bit of sky here. That's probably because our turtle didn't end where it started. Let's try 70 instead.

```python codeanim flower-5
click((330, 454), count=2)
write('72')
rerun()
```

Ooops. We're missing one petal now. Let's try 72. Great. That's perfect.

```python codeanim stem-1
click((165, 404))
vscode.newline()
vscode.newline(above=True)
chrome.activate()
tap(Key.up, repeat=26)
vscode.activate()
write('madame_sue.color("SaddleBrown")\n')
write('madame_sue.goto(0, -500)')
rerun()
```

Now, for the finishing touch. We need to give the flower a stem. Let's make it this SaddleBrown color. And then, we'll draw a line straight down to the ground at 0, -500.

```python codeanim stem-2
click((280, 352))
tap(Key.down, modifiers=[Key.alt], repeat=5)
vscode.newline()
write('madame_sue.penup()\n')
write('madame_sue.goto(0, 0)\n')
write('madame_sue.pendown()')
rerun()
```

Ooops! Our flower got misplaced. And it's the wrong color now. Let's fix it. We need to move line 8 to here so that we are using the correct color for the flower. And then, Madame Sue needs to return to 0, 0 after drawing the stem. So type, `madame_sue.goto((0, 0))`. Rerun.

```python codeanim stem-3
click((165, 430))
vscode.newline(above=True)
write('madame_sue.goto(-50, 0)')
rerun()
```

Hmm. The stem is not in the center. Let's first go to the center of the flower before we draw the stem down to the ground.

Wow. Look at this turtlerific masterpiece that Madame Sue has drawn!

# Outro

Today we learned how to use `if` statements to enable our turtles to make decisions.

What other conditions do you think we can use with `if` statements to make our turtles do different things? How about alternating the colors of our petals? Try it out and see what happens! And don't forget to share your ideas in the comments.

This video is the fourth in a series that gently introduces people to programming with Python and the turtle graphics library.

If you liked this video, hit the thumbs up. I'm The FriendlyTL and I make edutainment videos about software and open source apps that I also make. If you're interested in this kind of content, consider subscribing. Thanks for watching; I'll see you in the next one!
