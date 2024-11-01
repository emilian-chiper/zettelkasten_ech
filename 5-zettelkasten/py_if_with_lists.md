### Meta
2024-10-30 19:10
**Tags:** [[python]] [[py_basics]] [[py_conditionals]]
**Status:** #completed 

### Using if Statements with Lists
There are a variety of use cases for combining `if`  statements with lists:
- Watch for special values to be treated differently,
- Manage chaining conditions,
- Prove that your code works as expected in all possible situations,
- etc.

#### Checking for Special Items
```Python title:example.py
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']

for requested_topping in requested_toppings:
	print(f"Adding {requested_topping}.")

print("\nFinished making your pizza!")

"""
Adding mushrooms.
Adding green peppers.
Adding extra cheese.

Finished making your pizza!
"""
```

What if the pizzeria runs out of green peppers? An `if` statement inside the for loop can handle this situation:
```Python title:example.py
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']

for requested_topping in requested_toppings:
	if requested_topping == 'green peppers':
		print("Sorry, we're out of green peppers.")
	else:
		print(f"Adding {requested_topping}.")

print("\nFinished making your pizza!")

"""
Adding mushrooms.
Sorry, we're out of green peppers right now.
Adding extra cheese.

Finished making your pizza!
"""
```

#### Checking that a List is Not Empty
```Python title:example.py
requested_toppings = []

if requested_toppings:
	for requested_toppings in requested_toppings:
		print(f"Adding {requested_topping}.")
	print("\nFinished making your pizza!")
else:
	print("Are you sure you want a plain pizza?")

"""
Are you sure you want a plain pizza?
"""

```

#### Using Multiple Lists
```Python title:example.py
available_toppings = ['pepperoni', 'pineapple', 'green peppers', 'pepperoni', 'pineapple', 'extra cheese']

requested_toppings = ['mushrooms', 'french fries', 'extra cheese']

for requested_topping in requested_toppings:
	if requested_topping in available_toppings:
		print(f"Adding {requested_topping}.")
	else:
		print(f"Sorry, we're out of {requested_topping}.")

print("\nFinished making your pizza!")

"""
Adding mushrooms.
Sory, we don't have french fries.
Adding extra cheese.

Finished making your pizza!
"""
```
