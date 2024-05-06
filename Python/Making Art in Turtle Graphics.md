# Links

- Starting Code: https://github.com/shadanan/turtle/blob/main/art1.py
- Turtle Graphics Documentation: https://docs.python.org/3/library/turtle.html
- Hexagons are the Bestagons: https://www.youtube.com/watch?v=thOifuHs6eY

```python codeanim header
def rerun():
    click((974, 40))
    click((830, 102))
    wait()
def copy():
    click((165, 12))
    click((271, 118))
def paste():
    click((165, 12))
    click((271, 142))
```

# Intro

In our last video, we made this square. It's kind of bland though, don't you think? The background is white, and the turtle doesn't look like a turtle. It isn't even green! I promised you beautiful art, and this ain't it.

Today, we're going to play with the colors, and adjust the thickness of lines. We'll also make the turtle look like a turtle!

# New File

```python codeanim run
click((830, 102))
wait()
```

This is the code we wrote last time. It creates a turtle called Annie, and it draws this square. Let's reuse this code to make a much nicer looking square. Let's run it to remind ourselves what it does. Click the triangle button to run our program. And there is our square from last time!

If you didn't do the exercise from last time, I've linked the code in the description so that you can copy pasta.

# Appearance

```python codeanim shape
click((404, 222))
write('\nannie.shape("turtle")\n')
rerun()
```

The first thing we'll do is make Annie look like an actual turtle. To do this, we type `annie.shape("turtle")`. Remember that to run the program, we have to close the previous program. So, click the X, and then click the triangle button to rerun our program. Wow! Annie is no longer a poor arrow. She's a proper turtle now!

But, what other shapes could Annie be? To find out, the best way is to look at the instruction manual. We usually call this the documentation, or docs for short. No, not that kind of doc. This kind of doc. I've linked it in the description.

So according to the docs, the available shapes are arrow, turtle, circle, triangle, and classic. The default is classic.

```python codeanim size
vscode.activate()
write("annie.shapesize(5, 5, 12)\n")
rerun()
```

But notice down here that there's a method to change the size of our turtle! Let's use it to make Annie bigger! So we can just do as the docs say, and type, `annie.shapesize(5, 5, 12)`. Close and rerun. Whoa! Annie's a boss now. She's as big as our square.

```python codeanim smaller
click((341, 272))
write("\b2")
click((373, 272))
write("\b2")
rerun()
```

Maybe Annie's a little too big, let's make her a little smaller. Let's change the width and length size to be 2. Close and rerun. Annie's smaller, but no less of a boss.

# Colors

```python codeanim annie-green
click((165, 300))
write('annie.color("green")\n')
rerun()
```

I think the most popular color for a turtle is green. Let's make Annie green! Type, `annie.color("green")`. Close and rerun.

Interesting, not only did Annie become green, but the line she drew is also green! So, this is a way to set the color of the line that Annie draws.

```python codeanim ocean-blue
click((165, 196))
write('\nturtle.bgcolor("blue")\n')
rerun()
```

Now that Annie is green, let's make the background a different color. How about blue, like the ocean? To change the background color, we type `turtle.bgcolor("blue")`. Notice that we didn't say annie this time. That's because we want to affect the background color, which is different from the turtle. Close and rerun. Whoa. That blue is pretty serious.

```python codeanim show-color-tool
chrome.activate()
chrome.resize((700, 200), (500, 740))
chrome.navigate("https://shad.io/color/")
```

I think we need a different shade of blue. Here's a tool I made so that you can choose a color. What color you ask? Any color! This is better than any crayon or coloring pencil. You'll find the tool at shad.io/color/.

```python codeanim pick-ocean-color
chrome.activate()
click((964, 754))
click((1115, 600))
click((954, 860))
click((350, 222), count=2)
paste()
rerun()
```

This slider that looks like a rainbow lets you choose the color. And this box let's you pick various shades of the color. Okay, this here is a nice color for our ocean. Click the copy button, and double click `blue` to select it. Edit, paste. Close and rerun. That ocean color is a lot more pleasant, don't you think?

```python codeanim pick-annie-color
chrome.activate()
click((786, 754))
click((956, 350))
click((954, 860))
click((326, 352), count=2)
paste()
rerun()
```

Okay, that's pretty nice, but, I think Annie would like a makeover. We can make her any color. So how about this one? Click the copy button. Double click `green`. Edit, paste. Close and rerun. Wow! Look at that. Annie is living her best life!

# Line Thickness

But that square, it's kinda square, don't you think?

```python codeanim thicker
click((165, 378))
write('annie.width(5)\n')
rerun()
```

Let's start by making the lines thicker. Right here, we type `annie.width(5)`. Close and rerun. Annie and the square stand out a lot more now! That's great!

# Bringing Friends

So, Annie's been hard at work, but the best efforts in life are collaborations. Let's lend a hand.

We're going to introduce two new turtles, Anvi and Dima. And they're going to help Annie draw a masterpiece!

```python codeanim anvi
click((165, 611))
write('\nanvi = turtle.Turtle()\n')
write('anvi.shape("turtle")\n')
write('anvi.width(7)\n')
chrome.activate()
click((890, 754))
click((954, 860))
vscode.activate()
write('anvi.color("')
paste()
write('")\n')
rerun()
```

First, we create Anvi. We type `anvi = turtle.Turtle()`. Then we make Anvi's shape a turtle, and make the lines wider. Now, let's pick a color for Anvi. This one's cool. Ok, close, rerun.

Oh, interesting. Anvi appeared right on top of Annie. The reason for this is that every time we create a new turtle, they start at the same position which is coordinates (0, 0).

```python codeanim move-anvi
vscode.activate()
write('anvi.goto(0, 100)\n')
rerun()
```

Let's move Anvi so that both Annie and Anvi have their own space to work. So we type, `anvi.goto(0, 100)`. Close and rerun.

```python codeanim penup
vscode.activate()
tap(Key.up)
vscode.newline(above=True)
write('\nanvi.penup()')
tap(Key.down, repeat=2)
write('anvi.pendown()\n')
rerun()
```

Okay, that's not right. We need Anvi to move without creating a new line. So before we move, we type `anvi.penup()`, then we move Anvi, then we type `anvi.pendown()`.

```python codeanim dima
vscode.activate()
write('\ndima = turtle.Turtle()\n')
write('dima.shape("turtle")\n')
write('dima.width(10)\n')
chrome.activate()
click((1020, 754))
click((954, 860))
vscode.activate()
write('dima.color("')
paste()
write('")\n\n')
write('dima.penup()\n')
write('dima.goto(0, -200)\n')
write('dima.pendown()\n')
rerun()
```

Dima finally got his invitation to join the party. It was late in the mail. Classic! Well, Dima gets the same treatment. Set his shape, color, and give him some space to work as well.

# Drawing More Shapes

```python codeanim hexagon
vscode.activate()
vscode.jump(27)
write('\nanvi.forward(100)\n')
write('anvi.right(60)\n')
drag((165, 486), (165, 537))
copy()
click((165, 537))
paste()
tap("v", modifiers=[Key.cmd])
tap("v", modifiers=[Key.cmd])
tap("v", modifiers=[Key.cmd])
tap("v", modifiers=[Key.cmd])
rerun()
```

Now, we all know that hexagons are the bestagons! And Anvi is looking to get started! A hexagon has 6 equal sides, so we type `anvi.forward(100)` and then `anvi.right(60)`. We can copy paste these two lines 6 times. Btw, you can paste with the keyboard by pressing Ctrl+V or Cmd+V if you're on a Mac. Close and rerun. Oh no, Anvi's art is interfering with Annie's art.

```python codeanim bigger-hexagon
vscode.activate()
tap(Key.up, repeat=12)
tap(Key.right, modifiers=[Key.cmd])
tap(Key.left, repeat=2)
write("\b5")
tap(Key.down, repeat=2)
write("\b5")
tap(Key.down, repeat=2)
write("\b5")
tap(Key.down, repeat=2)
write("\b5")
tap(Key.down, repeat=2)
write("\b5")
tap(Key.down, repeat=2)
write("\b5")
rerun()
```

Let's make the hexagon bigger by changing 100 to 150. Close and rerun. Perfect!

Annie and Anvi's tasks are done, so Annie tells Dima to draw an octagon. Annie's allowed to give orders, because she's the boss.

```python codeanim octagon
vscode.activate()
vscode.jump(49)
write('\ndima.forward(200)\n')
write('dima.left(45)\n')
```

We start by having Dima move forwards by 200. These are giant steps so that the octagon fully surrounds the square and hexagon. Because Dima is below the other two turtles, he needs to turn left instead of right. And he'll turn 45 degrees to make an octagon.

```python codeanim copy-pasta
drag((165, 484), (165, 537))
tap("c", modifiers=[Key.cmd])
tap(Key.esc)
tap("v", modifiers=[Key.cmd], repeat=7)
rerun()
```

Octagons have 8 sides, so let's copy that code, and paste it 7 more times. You can type Ctrl+C to copy, or Cmd+C on a Mac. Close and rerun.

Look at that! With Anvi and Dima joining in, it’s a real art party now. I think it looks fantastic!

# Outro

So that was our video on making art using turtle graphics. We're now able to change the background color, the color and thickness of our lines and even the shape of our turtle!

You should now be able to make the most beautiful art. I'm curious to know what you end up making! Post your ideas in the comments!

This video is the second in a series that gently introduces people to programming using Python and the turtle graphics module.

If you liked this video, hit the thumbs up. I'm The FriendlyTL and I make edutainment videos about software and open source apps that I also make. If you're interested in this kind of content, consider subscribing. Thanks for watching; I'll see you in the next one!
