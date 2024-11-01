### Meta
2024-10-30 13:25
**Tags:** [[python]] [[py_basics]] [[py_conditionals]]
**Status:** #completed 

### Simple if Statements
```Python title:example.py
age = 19
if age >= 18:
	print("You are old enough to vote!")

"""
You are old enough to vote!
"""
```

Indentation plays the same role in `if` statements as it did in `for` loops. The same rules apply.

### if-else Statements
```Python title:example.py
age = 17
if age >= 18
	print("You are old enough to vote!")
else:
	print("Sorry, you are too young to vote.")

"""
Sorry, you are too young to vote.
"""
```

### The if-elif-else Chain
```Python title:example.py
age = 12
if age < 4:
	print("Your admission cost is $0.")
elif age < 18:
	print("Your admission cost is $25.")
else:
	print("Your admission cost is $40.")

"""
Your admission cost is $25.
"""
```

### Using Multiple elif Blocks
```Python title:example.py
age = 12

if age < 4:
	price = 0
elif age < 18:
	price = 25
elif age < 65:
	price = 40
else:
	price = 20

print(f"Your admission cost is ${price}.")

"""
Your admission cost is $25.
"""
```

### Omitting the else Block
Python doesn’t require an `else` block at the end of an `if-elif` chain.
```Python title:example.py
age = 12

if age < 4:
	price = 0
elif age < 18:
	price = 25
elif age < 65:
	price = 40
elif age >= 65
	price = 20

print(f"Your admission cost is ${price}.")

"""
Your admission cost is $25.
"""
```

### Testing Multiple Conditions
The `if-elif-else` chain is powerful, but it’s only appropriate to use when you just need one test to pass.

Sometimes it’s important to check all conditions of interest. If so, use a series of simple `if` statements.
```Python title:example.py
requested_toppings = ['mushrooms', 'extra cheese']

if 'mushrooms' in requested_toppings:
	print("Adding mushrooms.")
if 'pepperoni' in requested_toppings:
	print("Adding pepperoni.")
if 'extra cheese' in requested_toppings:
	print("Adding extra cheese.")

print("\nFinished making your pizza!")

"""
Adding mushrooms.
Adding extra cheese.

Finished making your pizza!
"""
```

This code wouldn’t work if we used an `if-elif-else` block, because the code would stop running after only one test passes.
```Python title:example.py
requested_toppings = ['mushrooms', 'extra cheese']

if 'mushrooms' in requested_toppings:
	print("Adding mushrooms.")
elif 'pepperoni' in requested_toppings:
	print("Adding pepperoni.")
elif 'extra cheese' in requested_toppings:
	print("Adding extra cheese.")

print("\nFinished making your pizza!")

"""
Adding mushrooms.

Finished making your pizza!
"""
```

The `'mushrooms'` condition passes, so the rest of the block is skipped.