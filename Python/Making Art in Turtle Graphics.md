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

Interesting, not only did Annie become green, but the line she drew is also green! So, this is a way to set the color of the line that Annie draws.

```python codeanim
write('turtle.bgcolor("blue")')
```

Now that Annie is green, let's make the background a different color. How about blue, like the ocean? To change the background color, we type `turtle.bgcolor("blue")`. Notice that we didn't say annie this time. That's because we want to affect the background color, which is different from the turtle. Close and rerun. Whoa. That blue is pretty serious.

I think we need a different shade of blue. Here's a tool I made so that you can choose a color. What color you ask? Any color! This is better than any crayon or coloring pencil. You'll find the tool at shad.io/color.

This slider that looks like a rainbow lets you choose the color. And this box let's you pick various shades of the color. Okay, this here is a nice color for our ocean. Click the copy button, and select `blue`. Edit, paste. Close and rerun. That ocean color is a lot more pleasant, don't you think?

Okay, that's pretty nice, but, I think Annie needs a makeover. We can make her any color. So how about this one? Click the copy button. Select `green`. Edit, paste. Close and rerun. Wow! Look at that. Annie is living her best life!

# Line Thickness

But that square, it's kind of thin, don't you think? And why are all the sides the same color?

What do you think about making the square thicker and giving each side a different color? Sounds fun, right? Let's do it!

```python codeanim
write('annie.width(5)')
```

Let's start by making lines thicker first. Right after we define Annie and before the forward commands, we type `annie.width(5)` as the docs say. This will make Annie and the lines she draws significantly thicker than the default we currently have. Close and rerun. Annie and the square stand out more now! That's great!

```python codeanim
write('annie.color("#ffd707")')
write('annie.forward(100)')
write('annie.right(90)')
write('annie.color("#ff3d00")')
write('annie.forward(100)')
write('annie.right(90)')
write('annie.color("#b62fa8")')
write('annie.forward(100)')
write('annie.right(90)')
write('annie.color("#59d0ea")')
write('annie.forward(100)')
```

Now let's change the color of each side of the square. To do this, we need to change Annie's color after she is done moving forward and right before she turns and makes a new move forward. So we type `annie.color("#ffd707")` before each turn and paste our color of choise. You can use the color tool to pick any color. I chose this shade of yellow, this shade of orange, this shade of purple and finally this shade of cyan. Close and rerun. Woah, that's cool! Annie draws each side of the square in a different color and this makes the square pop up even more!

# Bringing Friends

So, Annie has been busy at work with her colorful square. She's done such a great job, but look around, it's all so quiet. Do you think Annie might be feeling a bit lonely? I think so too. What do you say we call over some friends to help her out drawing?

Let's give Annie some company and introduce two new turtles: Anvi and Benny. They're going to help Annie with drawing and make a masterpiece!

```python codeanim
write('anvi = turtle.Turtle()')
write('benny = turtle.Turtle()')
write('anvi.shape("turtle")')
write('benny.shape("turtle")')
write('anvi.color("#ff1111")')
write('benny.color("#fff500")')
```

So, we create Anvi and Benny just like how we created Annie, we type `anvi = turtle.Turtle()` and `benny = turtle.Turtle()`. We'll set their shapes to 'turtle', `anvi.shape("turtle")` and `benny.shape("turtle")`. If you want, you can set them to any shape available. Let's make sure they look apart. Let's make Anvi red and Benny yellow, again up to you to pick any color from the color tool. So we type `anvi.color("#ff1111")` to set Anvi to red, then `benny.color("#fff500")` to set Benny to yellow. Close and rerun. Oh uh, where is Anvi and Benny?

When Anvi and Benny are created, they start at the center of the screen, which is the default starting position for any new turtle. This position is called the `home` position, and its coordinates are (0,0). Since all three turtles start at the home position they do overlap which makes it seem like only Annie is present.

To be able to see all the turtles on the screen, we need give Anvi and Benny a different starting positions so they don't start right on top of Annie. Let's move them a bit and position them slightly off to the sides so everyone has their own space. Let's move Anvi first.

```python codeanim
write('anvi.penup()')
write('anvi.goto(0, 100)')
write('anvi.pendown()')
```

According the the docs, to make turtle move to a different position without any lines, we need to type `anvi.penup()` followed by `anvi.goto(0, 100)` passing the coordinate where we want Anvi to stand on the screen. And finally `anvi.pendown()`. Close and rerun. Now we see Anvi.

The first command `penup()` lifts Anvi with her drawing pen. This way, it won't leave any lines while moving to her position. The second command `goto(x, y)` is where we want to place her on the screen. I wanted Anvi to live upstairs Annie so I only moved her vertically by a distance of 100. Once Anvi is at her new spot, the last command `pendown()` puts Anvi's drawing pen back down on the playground to allow her to draw again.

```python codeanim
write('benny.penup()')
write('benny.goto(0, -100)')
write('benny.pendown()')
```

Now that we moved Anvi, let's move Benny too, I want Benny to show up bellow Annie and Anvi! We type `benny.penup()` then `benny.goto(0, 200)` and finally `benny.pendown()`. Close and rerun. Now we can see all of our three turtles! We just created Anvi and Benny! they're not just any turtles, they're Annie's artistic friends.

# Drawing More Shapes

Now that annie's friends are over let's make them join the game and have them draw a shape each.

```python codeanim
write('anvi.forward(100)')
write('anvi.right(60)')
write('anvi.forward(100)')
write('anvi.right(60)')
write('anvi.forward(100)')
write('anvi.right(60)')
write('anvi.forward(100)')
write('anvi.right(60)')
write('anvi.forward(100)')
write('anvi.right(60)')
write('anvi.forward(100)')
```

Anvi loves angles and sides. Let's make her draw a hexagon right around Annie's square. This will be like a big hug from Anvi to Annie! A hexagon has 6 equal sides, so we type `anvi.forward(100)` followed by `anvi.right(60)` repeated 6 times. Close and run. Oh no, that's not what I wanted, I wanted the hexagon to fit nicely around Annie's square. Let's make Anvi move forward by a larger distance to wrap aroud Annie. Let's change 100 to 150. Close and Rerun. That's awesome! isn't it?

```python codeanim
write('anvi.forward(150)')
write('anvi.right(60)')
write('anvi.forward(150)')
write('anvi.right(60)')
write('anvi.forward(150)')
write('anvi.right(60)')
write('anvi.forward(150)')
write('anvi.right(60)')
write('anvi.forward(150)')
write('anvi.right(60)')
write('anvi.forward(150)')
```

I bet Benny can’t resist joining in. Let's make him draw and octagon that wraps around both, Annie's square and Anvi's hexagon. An octagon has 8 sides, so we type `benny.forward(200)`, this time passing 200 to make him take giants steps so that he is able to wrap around both Annie and Anvi. Then we type `benny.right(60)`. We repeat this 8 times. Close and rerun. oh uh, why is Benny moving down?

```python codeanim
write('benny.forward(200)')
write('benny.right(45)')
write('benny.forward(200)')
write('benny.right(45)')
write('benny.forward(200)')
write('benny.right(45)')
write('benny.forward(200)')
write('benny.right(45)')
write('benny.forward(200)')
write('benny.right(45)')
write('benny.forward(200)')
write('benny.right(45)')
write('benny.forward(200)')
write('benny.right(45)')
write('benny.forward(200)')
```

Since we set Benny to move right, it will be turning opposit direction, so we need to make Benny turn left instead towards Annie and Anvi. let's fix that and change `right` to `left`. Close and rerun.

```python codeanim
write('benny.forward(200)')
write('benny.left(45)')
write('benny.forward(200)')
write('benny.left(45)')
write('benny.forward(200)')
write('benny.left(45)')
write('benny.forward(200)')
write('benny.left(45)')
write('benny.forward(200)')
write('benny.left(45)')
write('benny.forward(200)')
write('benny.left(45)')
write('benny.forward(200)')
write('benny.left(45)')
write('benny.forward(200)')
```

Look at that! With Anvi and Benny joining in, it’s a real art party now. Annie isn't lonely anymore. Instead, she's right at the center of a colorful, fun gathering. Doesn't that look fantastic?

# Drawing any gon

After seeing Annie, Anvi and Benny drawing shapes with different numbers of sides and turn angles, you might be wondering if we can draw other shapes with different number of sides, Guess what? We absolutely can! Now you maybe wondering ok, if that's possible how do I know how much the turning angle is? Don't you worry, I got you covered!

All the shapes we’ve drawn are types of polygons. A polygon is a shape with straight sides. The square has 4 sides, the hexagon has 6, and the octagon has 8. We can make a polygon with any number of sides we want! here is a picture of other different polygons: we have a Pentagon, a Heptagon, a Nonagon and a Decagon! in fact, you can make a gon with any number of sides you want, you only need to decide on the number of side in advance!

And the angles you are asking! Here's a little trick about drawing polygons: to find out how much to turn the turtle at each corner, you divide 360 degrees by the number of sides. Why 360 degrees? Because a full turn, a complete circle around, is 360 degrees. So if you want to draw a square, 4 sides, you divide 360 by 4, which equals 90 degrees. That’s why our turtle turns 90 degrees at each corner of the square. For a hexagon, 6 sides, 360 divided by 6 equals 60 degrees. For an octagon, 8 sides, 360 divided by 8 equals 45 degrees.

You want to test this out? Let's have Benny draw a pentagon instead of an octagon. A pentagon has 5 sides. Now that you know the trick, can you guess how much the turtle should turn at each corner? Pause the video and give a thought.

```python codeanim
write('angle = 360/5')
```

Let’s do the math together. First, we divide 360 by 5. This calculation tells us that the turtle should turn 72 degrees at each corner of the pentagon. We can have our program do this calculation for us. To do this, we say angle and set it to be equal to 360 divided by 5. To see the result of this calculation, we tell our program to print it for us to see. To do this we write `print(angle)`. Close and rerun. Great! We can see our angle value down here, but Benny is still doing around drawing an octagon. Let's fix that.

```python codeanim
write('benny.forward(200)')
write('benny.left(angle)')
write('benny.forward(200)')
write('benny.left(angle)')
write('benny.forward(200)')
write('benny.left(angle)')
write('benny.forward(200)')
write('benny.left(angle)')
write('benny.forward(200)')
write('benny.left(angle)')
write('benny.forward(200)')
write('benny.left(angle)')
write('benny.forward(200)')
write('benny.left(angle)')
write('benny.forward(200)')
```

Let me show you another cool trick. Now that we know we need to update Benny to turn by 72 degrees to draw a pentagon. Instead of typing 72, we can type `angle` instead since it holds the value 72. Amazing, isn't it? let's do it. Close and rerun. Here is a pentagon!

# Challenge: Create Your Own Polygon

Now that you know the secret formula, it's your turn to create your own awesome polygons! choose any number of sides, or you can pick any polygon you like from the picture linked in the discription. Do the math to find out the angle, and program your turtle to draw it.

I'm curious to see what will you create. A seven-sided heptagon? Maybe a ten-sided decagon? let me know in the comments!
