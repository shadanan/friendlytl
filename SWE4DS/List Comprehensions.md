# Intro

A list comprehension is a concise syntax for creating lists in Python.

In this video, we're going to learn a simple trick to determine when it's possible to use list comprehension syntax. And when it is possible, we'll learn how to turn a for-loop into a list comprehension and vice-versa. Okay, let's go!

# What is a List Comprehension?

```python codeanim
vscode.open("~/Workspace/swe4ds")
vscode.newfile()
vscode.save("comprehension.py")
```

Suppose you want to create a list of square numbers from 1 to 10.

```python codeanim
write('# For Loop\n')
write('squares = []\n')
write('for x in range(1, 11):\n')
write('squares.append(x**2)\n')
backspace()
write('print(squares)')
vscode.save()
vscode.toggle_terminal()
write('python3 comprehension.py\n')
```

Without a list comprehension, we would first create a squares list, then for-loop from 1 to 11, then append to squares the square of x. Finally, we print out the result. If we save and run, we see our list of squares.

Now, let's see how this looks as a list comprehension.

```python codeanim
vscode.toggle_terminal()
vscode.jump(5)
vscode.bottom(select=True)
write('\n# List Comprehension')
vscode.newline()
write('squares = [')
write('x**2')
write(' for x in range(1, 11)')
vscode.save()
```

So, first we create the squares list. Then we say, x^2 for x in range(1, 11).

Let's compare these two solutions. First off, notice that there is no append in the list comprehension. But, the value of the append does shows up here, right before the for loop.

# List Comprehension Intuition

Suppose we only want the even squares.

```python codeanim loop-if
vscode.jump(3)
vscode.newline()
write('if x**2 % 2 == 0:')
vscode.jump(5)
write('\t')
```

One way to do this is to add an if-statement checking that x^2 modulo 2 equals 0.

```python codeanim comp-if
vscode.jump(8, 38)
write(' if x**2 % 2 == 0')
vscode.save()
```

We can add the if-statement to the list comprehension as well.

Are you starting to see the pattern?

```python codeanim comp-format
vscode.jump(8, 12)
write('\n')
vscode.jump(9, 10)
write('\n')
vscode.jump(10, 27)
write('\n')
vscode.jump(11, 21)
write('\n')
backspace()
```

```python
even_times_tables = []
for x in range(10):
	for y in range(10):
	    if x * y % 2 == 0:
	        even_times_tables.append(x * y)

even_times_tables = [
	x * y
	for x in range(10)
	for y in range(10)
	if x*y % 2 == 0
]
```

How about if I format the list comprehension like this? Notice that the for loop and the if statement are in the same order as in the for loop. The only thing out of order is the value being added to the result.

# When Can a List Comprehension be Used?

In general, you can use a list comprehension whenever you have various nested for-loops and if-statements where the value being added to the comprehension occurs only once.
