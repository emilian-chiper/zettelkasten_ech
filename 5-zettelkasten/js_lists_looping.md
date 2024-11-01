### Meta
2024-10-29 17:45
**Tags:** [[python]] [[py_basics]] [[py_working_with_lists]]
**Status:** #completed 

### Looping Through an Entire List
When you want to do the same action with every item in a list, you can use Python’s `for` loop.

```Python title:example.py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(magician)
"""
	Output:
	alice
	david
	carolina
"""
```

#### A Closer Look at Looping
The set of steps is repeated once for each item in the list, no matter how many there are.

You can choose any name for the temporary variable that will be associated with each value in the list. However, it’s helpful to choose a meaningful name (e.g., `for cat in cats:`).

#### Doing More Work with a for Loop
```Python title:example.py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
```

You can write as many lines of code as you like in the `for` loop. Each independent line following the `for` statement is considered *inside the loop*, and each indented line is executed once for each value in the list.

```Python title:example.py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
	print(f"I can't wait to see your next trick, {magician.title()}.\n")

"""
	Output:
Alice, that was a great trick!
I can't wait to see your next trick, Alice.

David, that was a great trick!
I can't wait to see your next trick, David.

Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.
"""
```

#### Doing Something After a for Loop
Any lines of code after the `for` loop that are not indented are executed once without repetition.
```Python title:example.py
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
	print(f"I can't wait to see your next trick, {magician.title()}.\n")

print("Thanks, everyone. That was a great magic show")

"""
	Output:
Alice, that was a great trick!
I can't wait to see your next trick, Alice.

David, that was a great trick!
I can't wait to see your next trick, David.

Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.

Thanks everyone, that was a great magic show.
"""
```