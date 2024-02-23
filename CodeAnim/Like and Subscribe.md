```python codeanim
set_delays(tap=0.05, end=0)
clear_editor()

write("\n\n\n\n\n\n\n\n\n")
paste("# 💌💌💌💌💌💌💌💌💌💌💌\n")
write("# Like and Subscribe\n")
paste("# 💌💌💌💌💌💌💌💌💌💌💌\n")

move(lines=-2)
for case in range(20):
    with no_delays():
        tap(Key.left, modifiers=[Key.cmd])
        move(cols=2)
    for i, char in enumerate("Like and Subscribe"):
        with no_delays():
            move(cols=1)
            backspace()
        write(char.upper() if case % 2 == 0 else char)
```

That's it for demo day. Links to CodeAnim are available in the description. Thanks for watching!
