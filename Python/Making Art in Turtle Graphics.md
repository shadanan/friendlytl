# Intro

In our last video, we made this square. It's kind of bland though, don't you think? The background is white, and the turtle doesn't look like a turtle. It isn't even green! I promised you beautiful art, and this ain't it.

Today, we're going to play with the colors, and adjust the thickness of lines. We'll also make the turtle look like a turtle!

# New File

This is the code we wrote last time. It creates a turtle called Annie, and it draws this square. Let's reuse this code to make a much nicer looking square.

So first, let's select this code, and click Edit, Copy.

Now, let's create a new file. Click File, New File, Python File.

Paste our previous code. Edit, Paste.

And let's save it. File, Save. And we'll name it pretty.py. Save. Let's make sure that it runs. Click the triangle. And there is our square from last time!

# Appearance

```python codeanim
write('annie.shape("turtle")')
```

The first thing we'll do is make Annie look like an actual turtle. To do this, we type `annie.shape("turtle")`. Remember that to run the program, we have to close the previous program. So, click the X, and then click the triangle button to rerun our program. Wow! Annie is no longer a poor arrow. She's a proper turtle now!

But, what other shapes could Annie be? To find out, the best way is to look at the instruction manual. We usually call this the documentation, or docs for short. No, not that kind of doc. This kind of doc. I've linked it in the description.

So according to the docs, the available shapes are arrow, turtle, circle, triangle, and classic. The default is classic (that's for you Dima).

```python codeanim
write("annie.shapesize(5, 5, 12)")
```

But notice down here that there's a method to change the size of our turtle! Let's use it to make Annie bigger! So we can just do as the docs say, and type, `annie.shapesize(5, 5, 12)`. Close and rerun. Whoa! Annie's a boss now. She's as big as our square.

Maybe Annie's a little too big, let's make her a little smaller. Let's change the width and length size to be 2. Close and rerun. Annie's smaller, but no less of a boss.

# Colors

```python codeanim
write('annie.color("green")')
```

I think the most popular color for a turtle is green. Let's make Annie green! Type, `annie.color("green")`. Close and rerun.

Interesting, not only did Annie become green, but the line she drew is also green! So this is a way to set the color of the line that Annie draws.

```python codeanim
write('turtle.bgcolor("blue")')
```

Now that Annie is green, let's make the background a different color. How about blue, like the ocean? To change the background color, we type `turtle.bgcolor("orange")`. Notice that we didn't say annie this time. That's because we want to affect the background color, which is different from the turtle. Close and rerun. Whoa. That blue is pretty serious.

I think we need a different shade of blue. Here's a tool I made so that you can choose a color. What color you ask? Any color! This is better than any crayon or coloring pencil.

This slider that looks like a rainbow lets you choose the color. And this box let's you pick various shades of the color. This here is a nice shade of color for our ocean. Copy this value, and replace `blue` with our new value. Close and rerun. That ocean color is a lot more pleasant, don't you think?

Okay, that's pretty nice, but, I think Annie needs a makeover. We can make her any color. So how about this one? Copy, paste. Close and rerun. Wow! Look at that. Annie is living her best life!

# Line Thickness

But that square, it's kind of thin, don't you think? And why are all the sides the same color?
