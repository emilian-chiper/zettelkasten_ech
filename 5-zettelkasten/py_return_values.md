### Meta
2024-11-01 12:30
**Tags:** [[python]] [[py_basics]] [[py_functions]]
**Status:** #completed 

### Return Values
A function doesn’t always have to display its output directly. Instead, it can process some data and then return a value or a set of values. That is known as a *return value*.

The `return` statement takes a value from inside a function and sends it back to the line that called the function.

#### Returning a Simple Value
```Python title:example.py
def get_formatted_name(first_name, last_name):
	"""Return a full name, neatly formatted."""
	full_name = f"f{first_name} {last_name}"
	return full_name.title()

musician = get_formatted_name('jimi', 'hendrix')
print(musician) # Jimi Hendrix
```

#### Making an Argument Optional
```Python title:example.py
def get_formatted_name(first_name, last_name, middle_name='')
	"""Return a full name, neatly formatted."""
	if middle_name:
		full_name = f"{first_name} {middle_name} {last_name}"
	else:
		full_name = f"{first_name} {last_name}"
	return full_name.title()

musician = get_formatted_name('jimi', 'hendrix')
print(musician) # Jimi Hendrix

musician = get_formatted_name('john', 'hooker', 'lee')
print(musician) # John Lee Hooker
```

#### Returning a Dictionary
```Python title:example.py
def build_person(first_name, last_name):
	"""Return a dictionary of information about a person."""
	person = {'first': first_name, 'last': last_name}
	return person

musican = build_person('jimi', 'hendrix')
print(musican)

"""
{'first': 'jimi', 'last': 'hendrix'}
"""
```

You can extend this function to accept optional values:
```Python title:example.py
def build_person(first_name, last_name, age=None):
	"""Return a dictionary of information about a person."""
	person = {'first': first_name, 'last': last_name}
	if age:
		person['age'] = age
	return person

musician = build_person('jimi', 'hendrix', age=27)
print(musician)

"""
{'first': 'jimi', 'last': 'hendrix', 'age': 27}
"""
```

`None` can serve as a placeholder value. In conditional tests, `None` evaluates to `False`.

#### Using a Function with a While Loop
```Python title:example.py
def get_formatted_name(first_name, last_name):
	"""Return a full name, neatly formatted."""
	full_name = f"{first_name} {last_name}"
	return full_name.title()

while True:
	print("\nPlease tell me your name: ")
	print("(enter 'q' at any time to quit)")

	f_name = input("Frist name: ")
	if f_name == 'q':
		break

	l_name = input("Last name: ")
	if l_name == 'q':
		break

	formatted_name = get_formatted_name(f_name, l_name)
	print(f"\nHello, {formatted_name}!")

"""
Please tell me your name:
(enter 'q' at any time to quit)
First name: eric
Last name: clapton

Hello, Eric Clapton!

Please tell me your name:
(enter 'q' at any time to quit)
First name: q
"""
```