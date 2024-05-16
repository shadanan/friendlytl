# Link:
- https://docs.python.org/3/library/turtle.html#turtle.speed

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

In our last video, we learned how to use for-loops to make our code simpler. We saw how our turtle Keith was able draw a whole spiral with just a few lines of code thanks to the power of for-loops. It was like we gave him a list of things to do over and over again, and he he executed it flawlessly.

But wait, what if we want Keith to vary his action depending on what's happening? What if we want him to switch the color to blue when his distance is exceeds than 200, and change to a different color if distance surpasses 400? 

That's where `if` statements come into play! `if` statements are like special rules we add to our code that allow us to make make decisions based on certain conditions. They function much like our everyday decisions: if we’re hungry, we eat; if it's cold outside, we wear a coat. Similarly, in programming, `if` statements help our code choose actions based on varying conditions.

Today, We're going to discover how to use `if` statements to make our code flexible and give our turtles even more powerful and dynamic capabilities! 

# If statement

This is the code we wrote last time. Let's run it again to make sure everything is working correctly.

That spiral is quite impressive, isn’t it?

```python codeanim square
vscode.activate()
write('\nif distance > 100:\n')
write('keith.color("#00c0ff")\n')
write('keith.width(10)\n')
```

Now, if we want to enable Keith to change color to blue when distance exceeds 200, we need to add an `if` statement to checks the distance each time we loop.

Type `if distance > 200:` new line `keith.color("#00c0ff")` then new line. Notice that the command under if is also idented. This `if`statement is kinda like Keith asking a question about the distance. If the answer is "yes," he changes color. If the answer is "no," he does nothing  continues moving forward and turning as usual. Close and rerun.

Wow, the spiral looks even cooler with the new colors!

# if-else Statements: More Decisions!

Okay, let's keep experimenting with `if` statement to make new art. 

Our adventure with Keith has come to an end. We will remove this code, but don’t worry—if you need to refer back to it, the link will be available in the description.

Now, let’s welcome Madame Sue. Madame Sue wants to draw a vibrant flower. She plans to alternate the petal colors between red and yellow to make the flower really stand out. Let's help her figure out how to create this colorful masterpiece!

```
write('turtle.bgcolor("#043c4d")\n')
write('madame_sue = turtle.Turtle()\n')
write('madame_sue.shape("turtle")\n')
write('madame_sue.width(5)\n')
write('madame_sue.color("#7df582")\n')
```

First, let's set the stage for Madame Sue to create her masterpiece. Start with the background `turtle.bgcolor("#043c4d")`. Let's choose a soothing light blue color for it. Then, let's bring our artist turtle, Madame Sue, into the picture. Type `madame_sue = turtle.Turtle()` to create her. Next, give her a turtle shape with `madame_sue.shape("turtle")`.

Now, let's adjust the appearance of her path. Set the width of her line `madame_sue.width(6)`, to make her drawings more visible. Then let's choose a vibrant color for Madame Sue; here, I'm choosing this fresh spring green `madame_sue.color("#7df582")`. Feel free to pick any color that you think will make her artwork pop!

```
write('for i in range(100):\n')
write('madame_sue.forward(100)\n')
write('if i % 2 == 0:\n')
write('madame_sue.right(170)\n')
write('else:\n')
write('madame_sue.left(160)\n')
```

Let's help Madame Sue draw her beautiful flower, we know that in order to draw a flower she needs spin around in a circular motion alternating between different turn angles for each petal. To do this, we use a loop to tell our program to repeat the instructions several times. So we type `for i in range(50)` 

Next let's have Madame Sue move forward by 100 units each iteration. Type `madame_sue.forward(100)` . Now, to alternate her turning angles, we need to set rules that tell her when to turn right and when to turn left. Can you think of how we might do this using if statements?

Here is an idea! Let's have Madame Sue turn right by 170 degrees if the current step number `i` is even i % 2 == 0. To do this we check if a number is even by seeing if the remainder when divided by 2 is 0, which we can write as `if i % 2 == 0:` new line `madame_sue.right(170)`.

Then we can have Madame Sue turn left by 160 degrees if the step number is odd. To do this we use an `else` statements to specify what should happen when the condition in the if statement isn't met which in our case, when i is odd. So we type new line `else:`, then new line `madame_sue.left(160)`. `if-else` statements give us even more options for decision making!

Great! I random choose the turning angle, I'm hoping this variation in angles will help us creates an intricate pattern resembling a flower. We can always keep experimenting with different angles to get various petal shapes. Let's run our program to see what happen. Close and rerun. 


```
write('100')
write('madame_sue.speed(0)\n')
```

Uh oh, what happened? why did Madame Sue stop? She was so close to finishing her drawing. It looks like we need to increase the number in `range()` to allow her to complete the flower. Let's change 50 to 100. 


By the way, we can also speed uo the drawing by typing `madame_sue.speed(0)`. Setting the speed to 0 makes her move as fast as possible. I have linked the documentation bellow for you to to explore different speeds.

```
write('madame_sue.color("#fa0000")\n')
write('madame_sue.color("#faf000")\n')
```


Wow, this is looking great!Let's help Madame Sue fulfill her wish of drawing a colorful flower. If the petal number `i` is even, Madame Sue draws a red petal, else if the petal number `i` is odd, Madame Sue draws a yellow one. Let's add the commands to under the conditions we have set. So we pick the color red then type ` madame_sue.color("#fa0000")` under the first condition, then pick the yellow color and type `madame_sue.color("#faf000")` under the second condition . Close and rerun.

This is so pretty! Madame Sue has successfully drawn a colorful flower just as she wanted. 


# Outro

Today we learned how to use an `if` statements to make our code flexible by making our turtles make decisions based on different conditions. We also saw how to use an `if` statements to help Madame Sue draw a colorful flower.

Can you think of other conditions we can use with if statements to make our turtles do different things? Remember, you can use if and if-else statements to create all sorts of amazing artwork! drawing different shapes, change colors, and so much more! Try it out and see what happens. Don't forget to share your ideas in the comments below!

This video is the forth in a series that gently introduces people to programming with Python and the turtle graphics library.

If you liked this video, hit the thumbs up. I'm The FriendlyTL and I make edutainment videos about software and open source apps that I also make. If you're interested in this kind of content, consider subscribing. Thanks for watching; I'll see you in the next one!
