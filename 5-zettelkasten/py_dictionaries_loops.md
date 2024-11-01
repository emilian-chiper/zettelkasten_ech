### Meta
2024-10-31 09:52
**Tags:** [[python]] [[py_basics]] [[py_dictionaries]]
**Status:** #pending 

### Looping Through All Key-Value Pairs
```Python title:example.py
user_0 = {
	'username': 'efermi',
	'first': 'enrico',
	'last': 'fermi',
}

for key, value in user_0.items():
	print(f"\nKey: {key}")
	print(f"Value: {value}")

"""
Key: username
Value: efermi

Key: first
Value: enrico

Key: last
Value: fermi
"""
```

Another example:
```Python title:example.py
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'rust',
	'phil': 'python',
}

for name, language in favorite_languages.items():
	print(f"{name.title()}'s favorite language is {language.title()}.")

"""
Jen's favorite language is Python.
Sarah's favorite language is C.
Edward's favorite language is Rust.
Phil's favorite language is Python.
"""
```

### Looping Through All the Keys in a Dictionary
```Python title:example.py
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'rust',
	'phil': 'python',
}

for name in favorite_languages.keys():
	print(name.title())

"""
Jen
Sarah
Edward
Phil
"""
```

Looping through the keys is actually the default behavior when looping through a dictionary, so this code would have the same output if you wrote:
```Python title:example.py
for name in favorite_languages:
```

You can access the value associated with any key you care about inside the loop, by using the current key:
```Python title:example.py
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'rust',
	'phil': 'python',
}

friends = ['phil', 'sarah']
for name in favorite_languages.keys():
	print(f"Hi {name.title()}.")

	if name in friends:
		language = favorite_languages[name].title()
		print(f"\t{name.title()}, I see you love {language}!")

"""
Hi Jen.
Hi Sarah.
	Sarah, I see you love C!
Hi Edward.
Hi Phil.
	Phil, I see you love Python!
"""
```

You can also use the `keys()` method to find out if a particular person was polled.
```Python title:example.py
"""
favorite_languages = {
	--snip
}
"""

if 'erin' not in favorite_languages.keys():
	print("Erin, please take our poll!")A

"""
Erin, pelase take our poll!
"""
```

The `keys()` method isn’t just for looping: it actually returns a sequence of all the keys, and the `if` statement simply checks if `erin` is in this sequence.

#### Looping Through a Dictionary’s Keys in a Particular Order
```Python title:example.py
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'rust',
	'phil': 'python',
}

for name in sorted(favorite_languages.keys()):
	print(f"{name.title()}, thank you for taking the poll.")

"""
Edward, thank you for taking the poll.
Jen, thank you for taking the poll.
Phil, thank you for taking the poll.
Sarah, thank you for taking the poll.
"""
```

#### Looping Through All Values in a Dictionary
```Python title:example.py
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'rust',
	'phil': 'python',
}

print("The following languages have been mentioned:")
for language in favorite_languages.values():
	print(language.title())

"""
The following languages have been mentioned:
Python
C
Rust
Python
"""
```

This does however show duplicates. To see each language chosen without repetition, we can use a set. A *set* is a collection in which each item must be unique:
```Python title:example.py
"""
favorite_languages = {
	--snip--
}
"""

print("The following languages have been mentioned:")
for language in set(favorite_languages.values()):
	print(language.title())

"""
The following languages have been mentioned:
Python
C
Rust
"""
```

When you wrap `set()`  around a collection of values that contains duplicates, Python identifies the unique items in the collection and builds a set from those items.

##### Building sets directly
```Python title:example.py
languages = {'python', 'rust', 'python', 'c'}
print(languages); # {'rust', 'python', 'c'}
```