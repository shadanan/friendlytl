```python codeanim header
def close():
    click((974, 40))
def run():
    click((830, 102))
    wait()
def rerun():
    click((974, 40))
    click((830, 102))
    wait()
```

# Intro

In our last video, our turtles, Annie, Anvi and Dima took turns drawing some cool shapes. Annie started off by drawing an orange square. Then, Anvi drew a green hexagon around Annie's square. And Dima it up by drawing an octagon around everything.

Perhaps you noticed that our code got quite long. We used copy paste to copy pasta code to draw the sides of our shapes. But suppose I wanted to describe to you how to draw a square.

I might say, draw a line, turn 90 degrees to the right, then do it again, and again a third time, and once more, and you'll end up back where you started. Another way I could describe it would be, draw a line, turn 90 degrees, and do those steps 4 times in total. This is a much simpler way to describe how to draw a square.

We can do the same thing in Python using a for-loop. For-loops help us make our code simpler by avoiding repetition. Today, we are going to discover how to use a for-loop to make our code simpler!

# For-Loop

```python codeanim new-file
vscode.activate()
vscode.jump(13)
run()
```

This is the code we wrote last time. Let's run it again to remind ourselves what it did. Nice. There our turtles drawing our three shapes.

Now, let's have Annie draw a square again, but smarter this time! Notice how we tell annie to move forwards 4 times, and to turn right 3 times? Well, let's modify this code do it with a for loop instead.

```python codeanim square
tap(Key.down, repeat=5, modifiers=[Key.shift])
tap(Key.backspace)
tap(Key.up, repeat=3)
write('\nfor side in range(4):')
tap(Key.down)
tap(Key.left, modifiers=[Key.cmd])
tap(Key.tab)
tap(Key.down)
tap(Key.left, modifiers=[Key.cmd])
tap(Key.tab)
rerun()
```

To do this, we first select and delete the duplicated code. Then we type `for side in range(4):` here. Now, to tell Python that we want these two lines to be repeated in the loop, we indent them by placing our cursor here, and pressing tab.

In Python, we use a `for` loop to repeat an action multiple times. `range()` tells the computer how many times to repeat something. So `range(4)` repeats the loop 4 times, which is perfect for drawing a square with 4 sides.

`side` is a counter that keeps track of how many sides of the shape we've already drawn. So, first, side will be 0 when it is drawing the top, 1, when it is drawing the right side, 2 for the bottom, and 3 for the left side. Many programming languages are a little funny because they start counting at 0 instead of 1.

```python codeanim hexagon
vscode.jump(26)
```

Great! Now let's do the same for Anvi. Here is the spot that we'll be making our code change. If you want to try it yourself, pause the video and give it a try! If you're not at a computer, think about what the changes should be. Maybe say it out loud. Don't worry if there are people around!

```python codeanim hexagon-2
tap(Key.down, repeat=10, modifiers=[Key.shift])
tap(Key.backspace)
tap(Key.up, repeat=3)
write('\nfor side in range(6):')
tap(Key.down)
tap(Key.left, modifiers=[Key.cmd])
tap(Key.tab)
tap(Key.down)
tap(Key.left, modifiers=[Key.cmd])
tap(Key.tab)
rerun()
```

Okay, so, Anvi is making a hexagon, so we want to repeat lines 24 and 25 six times. Let's start by deleting 26 through 35. Then we type `for side in range(8):` and then we indent these two statements. Close and rerun. Great!

```python codeanim octagon
vscode.jump(48)
```

Dima's turn now! Look at all this code. That's 16 lines of code. When we're done for-looping it, it should only be 3. If you didn't get it last time, then 3rd time's a charm, right? Think about what we want to do and how many times we want to do it. Pause the video the puzzle it out for yourself!

```python codeanim octagon-2
tap(Key.down, repeat=14, modifiers=[Key.shift])
tap(Key.backspace)
tap(Key.up, repeat=3)
write('\nfor side in range(8):')
tap(Key.down)
tap(Key.left, modifiers=[Key.cmd])
tap(Key.tab)
tap(Key.down)
tap(Key.left, modifiers=[Key.cmd])
tap(Key.tab)
rerun()
```

Did you figure it out? Let's find out. So, we start by deleting the duplicated code. Then we type `for side in range(8):` and then we indent the statements. Close and rerun.

Notice that our code is much smaller and simpler! With a for-loop, it's always just three lines of code, no matter how many sides our shape has. Remember, smart coders find simple solutions to problems!

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
