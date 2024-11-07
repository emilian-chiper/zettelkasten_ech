### Meta
2024-11-01 22:31
**Tags:** [[python]] [[py_basics]] [[py_functions]]
**Status:** #completed 

### Passing an Arbitrary Number of Arguments
```Python title:example.py
def make_pizza(*toppings):
	"""Print the list of toppings that have been requested."""
	print(toppings)

make_pizza('pepperoni')
make_pizza('mushrooms', 'green peppers', 'extra cheese')

"""
('pepperoni')
('mushrooms', 'green peppers', 'extra cheese')
"""
```

The asterisk in the parameter name `*toppings` tells Python to make a tuple called `toppings`, containing all the values this function receives. Python packs the arguments into a tuple even if the function receives only one value.

```Python title:example.py
def make_pizza(*toppings):
	"""Summarize the pizza we are about to make."""
	print("\nMaking a pizza with the following toppings:")
	for topping in toppings:
		print(f"- {topping}")

make('pepperoni')
make('mushrooms', 'green peppers', 'extra cheese')

"""
Making a pizza with the following toppings:
- pepperoni

Making a pizza with the following toppings:
- mushrooms
- green peppers
- extra cheese
"""
```

#### Mixing Positional Arguments with Arbitrary Arguments
```Python title:example.py
def make_pizza(size, *toppings):
	"""Summarize the pizza we are about to make."""
	print(f"\nMaking a {size}-inch pizza with the following toppings:")
	for topping in toppings:
		print(f"- {topping}")

make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')

"""
Making a 16-inch pizza with the following toppings:
- pepperony

Making a 12-inch pizza with the following toppings:
- mushrooms
- green peppers
- extra cheese
"""
```

**Note:** You’re often see the generic parameter `*args`, which collects arbitrary positional arguments like this.

#### Using Arbitrary Keyword Arguments
```Python title:example.py
def build_profile(first, last, **user_info):
	"""Build a dict containing user info"""
	user_info['first_name'] = first
	user_info['last_name'] = last
	return user_info

user_profile = build_profile('albert', 'einstein',
							location='princeton',
							field='physics')
print(user_profile)

"""
{'location': 'princeton','field': 'phisics',
'first_name': 'albert', 'last_name': 'einstein'}
"""
```

**Note:** You’ll often see the parameter name `*kwargs` used to collect nonspecific keyword arguments.

