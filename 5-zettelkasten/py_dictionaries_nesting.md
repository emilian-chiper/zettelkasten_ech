### Meta
2024-10-31 11:49
**Tags:** [[python]] [[py_basics]] [[py_dictionaries]]
**Status:** #completed 

### Nesting
Sometimes you need to store multiple dictionaries in a list, or a list of items as a value in a dictionary. This is called *nesting*.

#### A List of Dictionaries
```Python title:example.py
alien_0 = {'color': 'green', 'points': 5}
alien_1 = {'color': 'green', 'points': 10}
alien_2 = {'color': 'red', 'points': 15}

aliens = [alien_0, alien_1, alien_2]

for alien in aliens:
	print(alien)

"""
{'color': 'green', 'points': 5}
{'color': 'green', 'points': 10}
{'color': 'red', 'points': 15}
"""
```

A more realistic example would involve more than three aliens with code that automatically generates each alien.
```Python title:example.py
# Make an empty list for storing aliens
aliens = []

# Generate 30 green aliens
for alien_number in range(30):
	new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
	aliens.append(new_alien)

# Show the first 5 aliens
for alien in aliens[:5]:
	print(alien)
print("...")

# Show how many aliens have been created
print(f"Total number of aliens: {len(aliens)}")

"""
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
...
Total number of aliens: 30
"""
```

Changing the colors of some aliens:
```Python title:example.py
# Make an empty list for storing aliens
aliens = []

# Generate 30 green aliens
for alien_number in range(30):
	new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
	aliens.append(new_alien)

for alien in aliens[:3]:
	if alien['color'] == 'green':
		alien['color'] = 'yellow'
		alien['speed'] = 'medium'
		alien['points'] = 10

# Show the first 5 aliens
for alien in aliens[:5]:
	print(alien)
print("...")

"""
{'color': 'yellow', 'points': 10, 'speed': 'medium'}
{'color': 'yellow', 'points': 10, 'speed': 'medium'}
{'color': 'yellow', 'points': 10, 'speed': 'medium'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
...
"""
```

You can even expand the loop with an `elif` block that turns yellow aliens into red ones.
```Python title:example.py
for alien in aliens[0:3]:
	if alien['color'] == 'green':
		alien['color'] = 'yellow'
		alien['speed'] = 'medium'
		alient['points'] = 10
	elif alien['color'] == 'yellow':
		alien['color'] = 'red'
		alien['speed'] = 'fast'
		alient['points'] = 15
```

#### A List in a Dictionary
```Python title:example.py
# Store information about a pizza being ordered
pizza = {
	'crust': 'thick',
	'toppings': ['mushrooms', 'extra cheese'],
}

# Summarize the order
print(f"You ordered a {pizza['crust']-crust pizza 
with the following toppings:"})

for topping in pizza['toppings']:
	print(f"\t{toppings}")

"""
You ordered a thick-crust pizza with the following toppings:
	mushrooms
	extra cheese
"""
```

You can nest a list inside a dictionary anytime you want more than one value to be associated with a single key in a dictionary.
```Python title:example.py
favorite_languages = {
	'jen': ['python', 'rust'],
	'sarah': ['c'],
	'edward': ['rust', 'go'],
	'phil': ['python', 'haskell'],
}

for name, languages in favorite_languages.items():
	print(f"\n{name.title()}'s favorite languages are:")
	for language in languages:
		print(f"\t{language.title()}")

"""
Jen's favorite languages are:
	Python
	Rust
Sarah's favorite languages are:
	C
Edward's favorite languages are:
	Rust
	Go
Phil's favorite languages are:
	Python
	Haskell
"""
```

**Note:** You should not nest lists and dictionaries too deeply. There’s likely a simpler solution for the problem other than deep nesting.

#### A Dictionary in a Dictionary
```Python title:example.py
users = {
	'aeinstein': {
		'first': 'albert',
		'last': 'einstein',
		'location:' 'princeton',
	},

	'mcurie': {
		'first': 'marie',
		'last': 'curie',
		'location': 'paris',
	},
	
}

for username, user_info in users.items():
	print(f"\nUsername: {username}")
	full_name = f"{user_info['first']} {user_info['last']}"
	location = user_info['location']

	print(f"\tFull name: {full_name.title()}")
	print(f"\tLocation: {location.title()}")

"""
Username: aeinstein
	Full name: Albert Einstein
	Location: Princeton
Username: mcurie
	Full name: Marie Curie
	Location: Paris
"""

```