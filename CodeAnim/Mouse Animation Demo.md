# Intro

Hello, I'm The Friendly TL and I make edutainment videos about open source software that I also make. My very first video was a demo day about CodeAnim. CodeAnim is an app that I made that types for me. That's the video there. I've provided link if you'd like to watch it.

I recently started a series of edutainment videos about programming in Python using Turtle Graphics. This series is intended for beginners.

Many of my other videos are not. For most of my videos, I've been covering topics that are pretty advanced. And for this audience, I mostly need my video demos to be snappy and fast. So, I lean pretty heavily on keyboard shortcuts.

But for my new series intended for beginners, I want to use the _mouse_ as much as possible. And most importantly, I want it to be easy for my viewers to be able to follow the mouse around and see where it clicks. So, I added mouse animation to CodeAnim.

Let's take a look at what it does, and see how it works!

# Demo

So, I think the best way to demo CodeAnim's new mouse functionality is to show how it was used for the Turtle Graphics tutorial.

On the left here, we have our editor where CodeAnim will write the turtle graphics commands. This empty space is where the turtle graphics window will appear when we run the code.

And down here where we'll run CodeAnim and see the commands it is executing.

Okay, let's start CodeAnim, and I'll walk you through what it's doing.

```python codeanim newfile
vscode.activate()
```

So the first thing we're going to do is create a new file. The first CodeAnim command ensures that VS Code is the current active window.

```python codeanim crosshair
click((118, 12))
tap("4", modifiers=[Key.cmd, Key.shift])
tap(Key.esc)
```

Then we click the File menu which is located at coordinates 118, 12. How do we know that? On a Mac, you can press Command+Shift+4 to take a screenshot; here's the CodeAnim command. And when you do that, this crosshair appears along with the current coordinates of the mouse in very tiny fonts. I'll do my best to magnify that in post. Anyway, once we've recorded the coordinates, we can dismiss the crosshair by pressing escape.

```python codeanim
click((232, 64))
click((380, 170))
```

Next we click on New File at coordinates 232, 64, then Python File at coordinates 380, 170.

```python codeanim code
write('''import turtle
from colorsys import hsv_to_rgb

turtle.bgcolor("#2C2C32")

squirtle = turtle.Turtle()
squirtle.speed(0)

squirtle.penup()
squirtle.goto(-50, 50)
squirtle.pendown()

for i in range(720):
color = hsv_to_rgb(i / 360 % 1, 0.5, 0.7)
squirtle.color(color)
squirtle.forward(100 + i)
squirtle.right(89)

\bturtle.done()
''')
```

Let's have CodeAnim quickly type out the code for a nice Turtle Graphics demo. In this demo, we have a turtle named squirtle that will draw a spiral graphic with changing colors.

```python codeanim save
click((118, 12))
click((232, 294))
write("art")
click((640, 632))
```

Next, let's save the file and run it. So, we click the File menu at coordinates 118, 12, then the Save menu item at coordinates 232, 294. Type art. And then click the Save button at coordinates 640, 632.

```python codeanim run
click((830, 102))
wait()
```

Finally, let's run our program. So, we'll click the Run button at coordinates 830, 102. And there's squirtle drawing the art. I think it's pretty incredible how such simple rules for the art can result in such pretty graphics.

```python codeanim move
move((200, 800))
```

Anyway, let's look at the mouse animations in more detail. For the next little bit, I'll animate the mouse starting from here, and have it stop here.

The default mouse animation is modeled after a damped spring. Think back to high-school physics! I don't want to get too sweaty about this, but as I talk about each animation, I'll display a graph of the model as a function of time here. The y-axis varies from 0 to 1, where 0 represents the start position of the mouse, and 1 represents the end position.

```python codeanim default
move((1440, 480), start=(200, 800), interpolator=Spring(gamma=10, omega=0))
```

By default, the model is over-damped, so the mouse starts off moving very quickly, then slows down as it approaches the target, and then stops.

```python codeanim underdamped
move((1440, 480), start=(200, 800), interpolator=Spring(gamma=4, omega=8))
```

However, if we change the parameters, here gamma is 4, and omega is 8, we can have the mouse overshoot the target, then return and stop. You can see the overshoot in the graph as a y-value that is greater than 1.

```python codeanim slow
move((1440, 480), start=(200, 800), interpolator=Spring(gamma=2, omega=1))
```

You can interpret gamma as speed, and omega as the amount of oscillation. So, if we set gamma to 2, and omega to 1, we can make the mouse move slowly, and have a small amount of overshoot.

```python codeanim sigmoid
move((1440, 480), start=(200, 800), interpolator=Sigmoid())
```

Completely unrelated to springs is another animation model that I made available in CodeAnim. This one is called Sigmoid. You can think of the Sigmoid function as being smooth. So, the mouse starts off slow, speeds up, and then slows down.

```python codeanim default
move((1440, 480), start=(200, 800), interpolator=Spring(gamma=10, omega=0))
move((1440, 480), start=(200, 800), interpolator=Spring(gamma=4, omega=8))
move((1440, 480), start=(200, 800), interpolator=Spring(gamma=2, omega=1))
move((1440, 480), start=(200, 800), interpolator=Sigmoid())
```

Let's watch all of those animations again.

# Outro

CodeAnim has become very useful to me. I use it to animate all my videos. And I publish every CodeAnim script to GitHub. You can find links to CodeAnim, as well as my scripts in the description. If you do give CodeAnim a try, I'd love to hear your thoughts in the comments.

If you liked this video, hit the thumbs up. I'm The FriendlyTL and I make videos about useful open source apps that I also make such as Cipherly, CodeAnim, and Hexly.

My intro to programming in Python series on turtle graphics is ongoing. If you're interested in that content, be sure to subscribe, and hit the bell!

Thanks for watching; I'll see you in the next one!
