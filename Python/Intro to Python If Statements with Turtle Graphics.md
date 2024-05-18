# Link:

- Turtle Graphics Documentation: https://docs.python.org/3/library/turtle.html#turtle.speed
- Color table: https://shad.io/tkcolors/

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

In our last video, we learned how to simplify repetitive tasks in our code using for-loops. We saw how our turtle, Keith was able to effortlessly draw a whole spiral with just a few lines of code thanks to the power of for-loops. It was as if we gave him a list of things to do over and over again, and he executed it flawlessly.

Now, let's say we want Keith to vary his action depending on what's happening around him? for example, if he has traveled a certain distance, we might want him to change his color to let us know he's halfway through drawing the spiral. 

That's where `if` statements come into play! `if` statements are like special rules we add to our code that allow us to make choices based on the situation we're faced with. They function much like our everyday decisions: if we’re hungry, we eat, if it's cold outside, we wear a coat. Similarly, in programming, `if` statements give our code the ability to choose different actions based on varying conditions.

Today, we're going to discover how to use `if` statements to make our code flexible and give our turtles even more powerful and dynamic capabilities!

# If statement

```python codeanim new-file
vscode.activate()
vscode.jump(13)
run()
```

This is the code we wrote last time. Let's run it again to make sure everything is working correctly.

The spiral is quite impressive, isn’t it?

```python codeanim if-distance
vscode.activate()
vscode.jump(10)
tap(Key.right, modifiers=[Key.cmd])
tap(Key.enter)
write('if distance > 100:\n')
write('keith.color("CornflowerBlue")\n')
rerun()
```

Okay, now if we want Keith to switch to blue when he's more than halfway through the spiral, we need to add an `if` statement to check the distance each time we loop.

Great! So we type `if distance > 250:`. By the way, we can reler the color using its name as well.  I have created this color table for you, so you can choose from all the different possible colors and get to know some cool color names as well. Let's select this `CornflowerBlue`. New line `keith.color("CornflowerBlue")`, past the color. Notice that the command under if is also idented. Let's close and rerun to see what will happen.

Wow, the spiral looks even cooler with the added color!

# if-else Statements: More Decisions!

Okay, let's keep experimenting with `if` statement to make new art.

Our adventure with Keith has come to an end. We will remove this code, but don’t worry—if you need to refer back to it, the link will be available in the description.

Now, let’s welcome Madame Sue. Madame Sue enjoys drawing and coloring, she wants to draw a vibrant flower. She plans to draw a flower by alternating the petal colors between colors to make the flower really stand out. Let's help her figure out how to create this colorful masterpiece!

```python codeanim madame-sue
vscode.jump(5)
tap(Key.down, repeat=10, modifiers=[Key.shift])
write('turtle.bgcolor("SkyBlue")\n')
write('\nmadame_sue = turtle.Turtle()\n')
write('madame_sue.shape("turtle")\n')
write('madame_sue.width(5)\n')
write('madame_sue.color("DeepPink")\n')
```

First, let's set the stage for Madame Sue to create her masterpiece. Starting with the background `turtle.bgcolor("SkyBlue")`. Bring up the color table again and choose a soothing light blue color. Then, let's bring our artist turtle, Madame Sue, into the picture. Type `madame_sue = turtle.Turtle()` to create her. Next, give her a turtle shape with `madame_sue.shape("turtle")`.

Now, let's adjust the appearance of her drawing pen. Set the width of her line `madame_sue.width(6)`, to make her drawings more visible. Then let's choose a nice color for Madame Sue, I want this Deep Pink, type `madame_sue.color("DeepPink")` and paste the color. Feel free to pick any color that you think will make Madame Sue's artwork pop!

```python
for i in range(50):
    madame_sue.forward(100)
    if i % 2 == 0:
        madame_sue.right(170)
    else:
        madame_sue.left(170)
```

Let's help Madame Sue draw her beautiful flower. Imagine how a flower spins around to display all its petals. So we need to have Madame Sue something similar. Have her walk in a special pattern to simulate a cirle. To mimic the pattern of petals around a flower, she will need to alternate between different turn angles to draw each petal. Since we're going to be drawing the petal over and over, we want to use a loop to tell our program to repeat the instructions several times. So we type `for i in range(50):`, Let's loop 50 times. We want to loop enough times to make our flower look full and pretty!

Next let's have Madame Sue move forward by let's say 100 units each iteration. Type `madame_sue.forward(100)`. Now, to alternate between turning angles, we need to establish rules that dictate when to turn right and when to turn left. Can you think of how we can instruct her when to turn which way using if statements?

Here is an idea! Let's have Madame Sue turn right by 100 degrees if the current step number `i` is even i % 2 == 0. We check if a number is even by seeing if the remainder when divided by 2 is 0, which we can write as `if i % 2 == 0:` new line `madame_sue.right(170)`.

But what if `i` is odd? Then we can have Madame Sue turn left by maybe 100 degrees. To do this we use an `else` statements to specify what should happen when the condition in the if statement isn't met, which in the case when i is odd. So we type new line `else:`, then new line `madame_sue.left(100)`. 

This is amazing!`if-else` statements give us even more options for decision making!

Great! I have randomly choosen these turning angles, I'm hoping this variation in angles will help us creates an intricate pattern resembling a flower. We can always experiment with different angles to get various petal shapes. Let's run our program to see what happens. 

```python
madame_sue.speed(0)
```

By the way, we can also speed uo the drawing by typing `madame_sue.speed(0)`. Setting the speed to 0 makes her move as fast as possible. I have linked the documentation bellow for you to to explore different speeds. Let's close and rerun.

```python 
madame_sue.setheading(85)
madame_sue.penup()
madame_sue.goto(-500, -520)
madame_sue.pendown()
```

Uh oh, what's this zigzag? this looks more like grass instead of a flower. Wait, we can actually make it look like grass! Let's change Madame Sue's drawing direction to have the grass peaks face upward and position it at the buttom of the screen. To do this we type `madame_sue.setheading(85)`. According to the documentation, 0 is east, 90 is north, 180 is west, 270 is south. Let's have Madame Sue start her first move slightly northeast, say by 85 degrees. Then `madame_sue.penup()`, `madame_sue.goto(-500, -520)`, and `madame_sue.pendown()`. Let's rerun!

```python
madame_sue.color("DarkGreen")
madame_sue.begin_fill()
for i in range(50):
    madame_sue.forward(100)
    if i % 2 == 0:
        madame_sue.right(170)
    else:
        madame_sue.left(170)
madame_sue.end_fill()        
```

Great! We can also fill the color in green to make it more resemble grass more closely. Bring up the color table, Wow, so many nice green shades. Let's choose this Dark Green. Type `madame_sue.color("DarkGreen")` and past Dark Green, and add `madame_sue.begin_fill()` before starting the loop and `madame_sue.end_fill()` after the drawing is done. 

```python
# Grass     
```

Now that we have grass let have Madame Sue try drawing a flowing again. Let's push the grass code  bellow and have Madame Sue start by drawing the flower first. This way, we can quickly adjust if something doesn't look right. 

```python
for i in range(50):
    madame_sue.forward(100)
    if i % 2 == 0:
        madame_sue.right(180)
    else:
        madame_sue.left(160)
```
Okay, copy past the code here and let's experiment with angles till we find the closest shape to a flower. This time, let's have Madame Sue turn right ` madame_sue.right(180)` by 180 when `i` is even and turn left by 160 `madame_sue.left(160)` when `i` is odd. Let's close and rerun.

```python
    madame_sue.left(170)
```

Hmm, it's not quite a flower shape yet. We need to make the petals stand out more. Let's see what happens when we change left to 170. 

Doesn't this look like a sun? Are you thinking what I'm thinking? make it look like a sun? Brilliant idea, isn't it. 

```python
madame_sue.color("Yellow")
madame_sue.penup()
madame_sue.goto(300, 300)
madame_sue.pendown()
for i in range(40)
```

Let's change the color to yellow and have Madame Sue draw it up in the left corner. We also can reduce the range to 40 since Madame Sue was tracing over the sun again. So type `madame_sue.color("Yellow")`, `madame_sue.penup()`, `madame_sue.goto(300, 300)` maybe by 300, 300, then `madame_sue.pendown()`. We make the sun smaller by moving forward only by 60 `madame_sue.forward(100)`. This give the illusion the sun is far away! Close and rerun. 

That's amazing! It seems like Madame Sue drew a beautiful sunny day. All we need now is some beautiful colorful flowers for this to be complete!

```python
madame_sue.color("DarkRed")
for i in range(50):
    madame_sue.forward(100)
    if i % 2 == 0:
        madame_sue.right(170)
    else:
        madame_sue.left(160)
```

Let's experiment again! Copy paste this code, add comments #Grass, #Sun to the code so we can easily identify which part of the code is responsible for drawing the sun and which part is for the grass. Let's change the drawing color to, let's see dark red? type `madame_sue.color("DarkRed")` and past the color. This time let's try a right angle of 170 `madame_sue.right(170)`. Let's see what we got this time!

```python 
for i in range(80)
```

Wow, it's starting to take the shpe of a flower, uh oh, what happened? why did Madame Sue stop? She was so close to finishing her drawing. It looks like we need to increase the loop time to allow her to complete the flower. Let's increase to 80 since she not far from where she started, we don't want her to trace over the flower. Let's rerun.

```python
madame_sue.color("DarkRed")
for i in range(80):
    madame_sue.forward(100)
    if i % 2 == 0:
        madame_sue.right(170)
    else:
        madame_sue.left(160)
```

Wow, this is looking great, we finally have a flower! Now, let's help Madame Sue fulfill her wish of drawing a colorful flower. Bring up the color table and set a rule, if the petal number `i` is even, Madame Sue draws a hein MediumPurple petal, else if the petal number `i` is odd, Madame Sue draws a DarkMagenta petal. Let's add the commands to under the conditions we have set. So we pick the color red then type `madame_sue.color("MediumPurple")` under the first condition, then pick the yellow color and type `madame_sue.color("DarkMagenta")` under the second condition. Let's also reduce the forward distance to make it look smaller and better fit in the artwork `madame_sue.forward(30)`. I'm excited to see what it looks like now!

This is so pretty! Madame Sue has successfully drawn a colorful flower just as she wanted and even more.

# Outro

Today we learned how to use an `if` statements to make our code flexible by making our turtles make decisions based on different conditions. We also saw how to use an `if` statements to help Madame Sue draw a masterpiece.

Can you think of other conditions we can use with if statements to make our turtles do different things? Maybe add more flowers? Remember, you can use if and if-else statements to create all sorts of amazing artwork! drawing different shapes, change colors, and so much more! Try it out and see what happens. Don't forget to share your ideas in the comments below!

This video is the forth in a series that gently introduces people to programming with Python and the turtle graphics library.

If you liked this video, hit the thumbs up. I'm The FriendlyTL and I make edutainment videos about software and open source apps that I also make. If you're interested in this kind of content, consider subscribing. Thanks for watching; I'll see you in the next one!
