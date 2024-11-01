### Meta
2024-10-29 17:56
**Tags:** [[python]] [[py_basics]] [[py_working_with_lists]]
**Status:** #pending 

### Avoiding Indentation Errors
Python uses indentation to determine how a line, or group of lines, is related to the rest of a program.

#### Forgetting to Indent
Always indent a line after the `for` statement in a loop.

```Python title:example.py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
print(magician)

"""
	Output:
  File "magicians.py", line 3
    print(magician)
    ^
IndentationError: expected an indent block after 'for' statement on line 2
"""
```

#### Forgetting to Indent Additional Lines
```Python title:example.py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
print(f"I can't wait to see your next trick, {magician.title()}.\n")

"""
Alice, that was a great trick!
David, that was a great trick!
Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.
"""
```

This is a *logical error*. The syntax is valid, but the code doesn’t produce the desired result.

#### Indenting Unnecessarily
If you accidentally indent a line that doesn’t need to be indented, Python informs you about the unexpected indent:
```Python title:example.py
message = "Hello Python world!"
	print(message)

"""
  File: "example.py", line 2
  print(message)
  ^
IndentationError: unexpected indent
"""
```

#### Indenting Unnecessarily after the Loop
If you accidentally indent code that should run after the loop has finished, that code will be repeated once for each item in the list. Sometimes, Python reports an error, but often it will result in a logical error.
```Python title:example.py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
	print(f"I can't wait to see your next trick, {magician.title()}.\n")

	print("Thank you everyone, that was a great magic show!")

"""
Alice, that was a great trick!
I can't wait to see your next trick, Alice.

Thank you everyone, that was a great magic show!
David, that was a great trick!
...
Thank you everyone, that was a great magic show!
"""
```

This is another logical error.

#### Forgetting the Colon
The colon at the end of a `for`  statement tells Python to interpret the next line as the start of a loop.
```Python title:example.py
magicians = ['alice', 'david', 'carolina']
for magician in magicians
	print(magicina)

"""
	Output:
  File "example.py", line 2
    for magician in magicians
                             ^
SyntaxErrro: expected ':'
"""
```