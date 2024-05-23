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
def paste():
    click((165, 12))
    click((271, 142))
```

# Intro

In our last video, our turtles, Annie, Anvi and Dima took turns drawing some cool shapes. Annie started off by drawing an orange square. Then, Anvi drew a green hexagon around Annie's square. And Dima wrapped it up by drawing an octagon around everything.

Perhaps you noticed that our code got quite long. We used copy paste to copy pasta lots of code to draw the sides of our shapes.

But suppose you were telling me how to do draw a square.

You'd probably say, draw a line, turn right, then do it again, and once more, and one last time, and you'll end up back where you started. Another way you could describe it would be, draw a line, turn to the right, then repeat those steps 4 times in total. This is a much simpler way to describe how to draw a square.

We can do the same idea in Python using a for-loop. For-loops help us make our code simpler by avoiding repetition. Today, we are going to discover how to use a for-loop to make our code simpler!

# For-Loop

```python codeanim new-file
vscode.activate()
vscode.jump(13)
run()
```

This is the code we wrote last time. Let's run it again to remind ourselves what it did. Nice. There our turtles drawing our three shapes.

Now, let's have Annie draw a square again, but smarter this time! Notice how we tell Annie to move forwards 4 times, and to turn right 3 times? Well, let's modify this code to do it with a for-loop instead.

```python codeanim square
vscode.activate()
tap(Key.down, repeat=5, modifiers=[Key.shift])
tap(Key.backspace)
tap(Key.up, repeat=3)
write('\nfor count in range(4):')
tap(Key.left, modifiers=[Key.cmd])
tap(Key.down)
tap(Key.tab)
tap(Key.left, modifiers=[Key.cmd])
tap(Key.down)
tap(Key.tab)
rerun()
```

To do this, we first select and delete the duplicated code. Then we type here, `for count in range(4):`. Now, to tell Python that we want these two lines to be repeated in the loop, we indent them by placing our cursor here, and pressing tab, and here, and tab again.

In Python, we use a for-loop to repeat an action multiple times. `range()` tells the computer how many times to repeat something. So `range(4)` repeats the loop 4 times, which is perfect for drawing a square with 4 sides.

`count` is a counter that keeps track of how many sides we've drawn so far. So, first, count will be 0 when it is drawing the top, 1, when it is drawing the right side, 2 for the bottom, and 3 for the left side. You might think that count should be 1 for the top, and 2 for the right side, and so on. But for reasons, many programming languages start counting at 0 instead of 1.

```python codeanim hexagon
vscode.activate()
vscode.jump(26)
```

Now let's do the same for Anvi. Here is the spot that we'll be making our code change. If you want to try it yourself, pause the video and give it a try! If you're not at a computer, think about what the changes should be. Maybe say it out loud. Don't worry if there are people around!

```python codeanim hexagon-2
tap(Key.down, repeat=10, modifiers=[Key.shift])
tap(Key.backspace)
tap(Key.up, repeat=3)
write('\nfor count in range(6):')
tap(Key.left, modifiers=[Key.cmd])
tap(Key.down)
tap(Key.tab)
tap(Key.left, modifiers=[Key.cmd])
tap(Key.down)
tap(Key.tab)
rerun()
```

Okay, so, Anvi is making a hexagon, so we want to repeat lines 24 and 25 six times. Let's start by deleting lines 26 through 35. Then we type `for count in range(6):` and then we indent these two statements. Close and rerun.

```python codeanim octagon
vscode.activate()
vscode.jump(39)
```

Great! Dima's turn now! Look at all this code. That's 16 lines of code. When we're done for-looping it, it should only be 3. If you didn't get it last time, then 3rd time's a charm, right? Think about what we need to do and how many times we need to do it. Pause the video and puzzle it out for yourself!

```python codeanim octagon-2
tap(Key.down, repeat=14, modifiers=[Key.shift])
tap(Key.backspace)
tap(Key.up, repeat=3)
write('\nfor count in range(8):')
tap(Key.left, modifiers=[Key.cmd])
tap(Key.down)
tap(Key.tab)
tap(Key.left, modifiers=[Key.cmd])
tap(Key.down)
tap(Key.tab)
rerun()
```

Did you figure it out? Let's find out. So, we start by deleting the duplicated code. Then we type `for count in range(8):` and then we indent the statements. Rerun.

Notice that our code is much smaller and simpler! With a for-loop, it's always just three lines of code, no matter how many sides our shape has. Remember, smart coders find simple solutions to problems!

# Drawing a Spiral

```python codeanim header2
def close():
    click((974, 40))
def run():
    click((830, 102))
    wait()
def rerun():
    click((974, 40))
    click((830, 102))
    wait()
def paste():
    click((165, 12))
    click((271, 142))
```

Okay, let's make some new art. We have a very enterprising turtle named Keith. And Keith wants to make a spiral.

```python codeanim clear
vscode.activate()
vscode.jump(5)
tap(Key.down, modifiers=[Key.cmd, Key.shift])
tap(Key.up, repeat=2, modifiers=[Key.shift])
tap(Key.left, modifiers=[Key.shift])
tap(Key.backspace)
vscode.jump(5)
```

To start out, we'll say "bye" to Annie, Anvi, and Dima and we'll delete all of our previous code. Don't worry, if you want to find it again, I've posted a link to the code down in the doobleydoo.

```python codeanim keith
write('keith = turtle.Turtle()\n')
write('keith.shape("turtle")\n')
write('keith.width(5)\n')
```

First, let's create Keith the turtle. Type `keith = turtle.Turtle()`. And of course, Keith should look like a turtle. So, type, `keith.shape("turtle")`. Let's set the width of our line. Type, `keith.width(5)`.

```python codeanim show-color-tool
write('keith.color("')
chrome.activate()
chrome.resize((700, 200), (500, 740))
chrome.navigate("https://shad.io/color/")
click((890, 754))
click((946, 356))
click((954, 860))
vscode.activate()
paste()
vscode.newline()
rerun()
```

And finally, let's give Keith a nice color. Type `keith.color("`. We can use my color picker to pick a color for Keith. Head over to shad.io/color/. I think this will be a good color for our turtle. Switch back to our editor, and paste the color. Let's see how our new canvas looks. Noice!

```python codeanim spiral-1
vscode.activate()
write('\nfor count in range(100):\n')
write('keith.forward(50)\n')
write('keith.right(60)')
rerun()
```

Okay, time to make a spiral. So, one way that we can get Keith to draw a spiral is to move forwards a bit, turn a bit, and do that over and over again. Let's start by making a for loop that loops 100 times. Type, `for count in range(100):`, then press enter. Then, `keith.forward(50)`, and finally, `keith.right(60)`. Let's see how that looks.

Cool, so there's Keith tracing a hexagon over and over again. If we want him to make a spiral, we have to do something different.

We need Keith to move a little further each time he moves forward. How can we do that? Pause the video and ponder for a moment. This is a little tricky and different from before. Because now, the code in our loop won't be the same every time. It's changing just a little bit!

```python codeanim spiral-2
click((360, 430), count=2)
write('count')
rerun()
```

But Keith has a cool trick up his sleve. You see, we have `count`, and that happens to be changing every loop. What if we used `count` as our distance? Let's try! Replace 50 with count. Let's see what happens this time.

Whoa! Isn't that interesting? We kind of have a hexagonal spiral going on. But the lines are smushed together. How can we fix this? The reason it's smushed together is that we're only moving one space further each time through the loop. We need to move more than one space. Any ideas? Hmm?

```python codeanim spiral-3
click((403, 430))
write(' * 2')
rerun()
```

Did you think of multiplying count by some number? If so, you're a genius! Let's try multiplying by two. So type, `* 2` and let's see what happens.

```python codeanim spiral-4
click((376, 404), count=2)
write('4, ')
write('500, ')
write('4')
click((231, 404), count=2)
write('distance')
drag((351, 430), (446, 430))
write('distance')
rerun()
```

Oh my goodness. This is so pretty! By the way, theres another way that we can do this, and it's built in to the range function. Let's say that we want Keith to start out moving forward 4 spaces, and then each time through the loop, we want to increase how far Keith travels also by 4 spaces. And lets say we want to do this until Keith is taking giant steps of 500 spaces.

To do that, we pass those 3 things here. So, initially, Keith will step forward `4` spaces, comma, until he is stepping `500` spaces, comma, with steps increasing by `4` spaces each time.

With this change, this will no longer be the `count` because this loop is now producing Keith's forward distance. So let's rename `count` to `distance`. And let's replace `count * 2` with distance. Rerun.

Wow. Look at that beautiful spiral.

# Outro

Today we learned how to use a for-loop to make our code simpler. We also saw how to use a for-loop to make a spiral.

You know, making a spiral without a for-loop would have been quite painful don't you think? Just imagine how you would have done a spiral without a for-loop. What would that code have looked like?

Can you think of any other things that we might draw using a for-loop? I'm curious to know what you come up with! Post your ideas in the comments!

This video is the third in a series that gently introduces people to programming with Python and the turtle graphics library.

If you liked this video, hit the thumbs up. I'm The FriendlyTL and I make edutainment videos about software and open source apps that I also make. If you're interested in this kind of content, consider subscribing. Thanks for watching; I'll see you in the next one!
