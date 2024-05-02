# Intro

In our last video, we drew some cool shapes like a hexagon, an octagon and a Pentagon. But did you notice that we wrote the same lines over and over again. That can get a bit repetitive and boring, right? Well, guess what? There's a special way in Python called a loop that can helps us avoid repeating ourselves!

Today, let's discover how a `for` loop can make our coding life much easier and fun!

# `for` loop

Let's start by drawing a hexagon again, but smarter this time!

```python codeanim
for side in range(6):
  write('anvi.forward(150)')
  write('anvi.right(60)')
```

We type `for side in range(6):` then, new line. See how we are now inside the for loop. Then type `write('anvi.forward(150)')` and `write('anvi.right(60)')`. Close and run. Amazing!

In Python, we use a `for` loop to repeat an action multiple times but with fewer lines of code. `range(6)` tells the computer how many times to repeat something. It create a list of of numbers from 0 to 5 (6 numbers in total). So the loop will run 6 times, which is perfect for drawing a hexagon with 6 sides.

Each pass through the loop. `side` is a counter that keeps track of how many sides of the shape we've already drawn. Each time the loop runs, side represents the next side of the shape we're going to draw.

Notice, the 2 lines of code are inside the for loop. We do this to tell Python which code belong to the loop. This way only the code inside will repeat.

So basically a for loop tell the computer "Keep doing these steps in order until you have made all 6 sides of the hexagon."

```python codeanim
for side in range(8):
  write('benny.forward(200)')
  write('benny.right(45)')
```

Now let's make Benny draw an Octagon again, but this time, with less work! So, we type `for side in range(8)` then new line then ` write('benny.forward(200)')` followed by `write('benny.right(45)')`. Close and rerun. That's great!

# Challenge: The Spiral Challenge

Fantastic job today! You've just learned how to use for loops to make your coding much simpler and to avoid repetition. Remember, smart coders are lazy coders, they make the computer do the hard work!

Now, it’s your turn to get creative. Try to use a for loop to make your turtle draw a spiral.
Here’s a hint: you can make the turtle move a little further each time it moves forward.
You can also play around with the turning angle to see what cool patterns you can create!
Can you make a spiral that looks like a snail's shell or maybe something wilder? Share your creations with us in the comments!

# Outro
