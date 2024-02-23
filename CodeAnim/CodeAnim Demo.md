# Introduction

```python codeanim start
delay.set(tap=0.05, end=0)
vscode.activate()
vscode.focus("codeanim.py")
pause(2)
```

```python codeanim intro
write("""# Hello, I'm the friendly TL. This is my first demo day!

# I wanted to make a demo about a cool new project I'm working on, but it's hard to
# do a demo without typos. I decided that there should be a tool that I can use to
# type for me.

# To my surprise, I couldn't find a suitable one, so I made CodeAnim. And it's producing
# the recording that you're watching right now!

# As you can see, it's typing for me at a constant rate.
""")
```

```python codeanim emojis
with delay(tap=0.1, end=0):
    write("\n# We can also slow down the typing rate. 🐢\n")
with delay(tap=0.02, end=0):
    write("\n# Or we can make it really fast! 🏃\n")
with delay(tap=0, keys={" ": 0.35}, end=2):
    write("\n# It can even be configured to type one word at a time. 🎉\n")
```

Let's have CodeAnim write a Python function that converts a percentage grade to a letter grade.

```python codeanim coding
delay.set(tap=0.02, end=2)
write("\n\ndef to_letter_grade(")  # Let's call our function to_letter_grade
write("percentage_grade):\n")      # And have it take a parameter called percentage_grade
write("# A: grade >= 90\n")        # A grade 90 or above is an A
write("# B: 80 <= grade < 90\n")   # Between 80 and 90 is a B
write("# C: 70 <= grade < 80\n")   # Between 70 and 80 is a C
write("# D: 60 <= grade < 70\n")   # Between 60 and 70 is a D
write("# F: grade < 60\n")         # And below 60 is an F
```

Ok, let's write the logic!

```python codeanim edit
vscode.jump(20, 5)                       # With CodeAnim, we can jump to line 20
vscode.end(select=True)                  # And replace the comment with
write("if percentage_grade >= 90:\n")    # if percentage_grade is >= 90
write('return "A"')                      # then return A
delay.set(tap=0.01, end=0.1)
vscode.jump(22, 5)
vscode.end(select=True)
write("elif percentage_grade >= 80:\n")  # Now lets let CodeAnim finish writing the code for us
write('return "B"')
vscode.jump(24, 5)
vscode.end(select=True)
write("elif percentage_grade >= 70:\n")
write('return "C"')
vscode.jump(26, 5)
vscode.end(select=True)
write("elif percentage_grade >= 60:\n")
write('return "D"')
vscode.jump(28, 5)
vscode.end(select=True)
write("else:\n")
write('return "F"\n\n')
```

```python codeanim test
delay.set(tap=0.02, end=2)
vscode.jump(32)   # Alright, let's test our code by printing out the letter grades for a few grades
write('print(f"to_letter_grade(95): {to_letter_grade(95)}")\n')  # Say, 95
write('print(f"to_letter_grade(75): {to_letter_grade(75)}")\n')  # 75
write('print(f"to_letter_grade(35): {to_letter_grade(35)}")\n')  # and 35
vscode.run()      # And we'll have CodeAnim execute our code for us.
```

And we can see that A, C, and F are printed out.

Okay, let's have CodeAnim add type hints for our function.

```python codeanim hints
vscode.toggle_panel()    # So, let's close the terminal,
vscode.jump(19, 37)      # And then position the cursor here at line 19, column 37
write(": float")         # Add the parameter type hint
vscode.move(cols=1)      # Move the cursor to the right
write(" -> str")         # Add the return value type hint
vscode.run()             # And rerun for good measure!
```

```python codeanim describe-1
vscode.toggle_panel()
vscode.focus("codeanim.md")  # Let's take a look at the CodeAnim script that generated this recording.
vscode.jump(1)
```

Our first command sets the global delay on every keystroke and for every command.

Then we call the `focus` command to open the file that CodeAnim will type in.

```python codeanim describe-2
vscode.jump(9)
```

Then we use the `write` command to begin typing.

```python codeanim describe-3
vscode.jump(23)
```

Here we see that we can set different delays and type slower, or faster, or pause on specific keystrokes, like space in this example.

```python codeanim describe-2
vscode.jump(84)
```

Let's jump down to the section where we added type hints to our letter-grade function.

Here we have a command to toggle the terminal panel closed. Then we use a `jump` command to position the cursor at a specific position. We see a couple more `write` commands to add the type hints. A `move` command to move the cursor. And a final `run` command to execute the script.
