### Meta
2024-10-31 08:59
**Tags:** [[python]] [[py_basics]] [[py_dictionaries]]
**Status:** #completed 

### Working with Dictionaries
A *dictionary* in Python is a collection of *key-value pairs*. Each *key* is connected to a *value*, and you can use a key to access the value associated with it. A key’s value can be a number, a string, a list, or even another dictionary. A *key-value pair* is a set of values associated with each other.

```Python title:example.py
alien_0 = {'color': 'green', 'points': 5}
```

#### Accessing Values in a Dictionary
```Python title:example.py
alien_0 = {'color': 'green'}
print(alien_0['color']) # green
```

You can have an unlimited number of key-value pairs in a dictionary.
```Python title:example.py
alien_0 = {'color': 'green', 'points': 5}

new_points = alien_0['points']
print(f"You just earned {new_points} points!")

"""
You just earned 5 points!
"""
```

#### Adding New Key-Value Pairs
```Python title:example.py
alien_0 = {'color': 'green', 'points': 5}
print(alien_0)

alien_0['x_position'] = 0
alien_0['y_position'] = 25
print(alien_0)
"""
	From line 2:
{'color': 'green', 'points': 5}
	From line 6:
{'color': 'green', 'points': 5, 'x_position': 0, 'y_position': 5}
"""
```

#### Starting with an Empty Dictionary
```Python title:example.py
alien_0 = {}

alien_0['color'] = 'green'
alien_0['points'] = 5

print(alien_0) # {'color': 'green', 'points': 5}
```

#### Modifying Values in a Dictionary
```Python title:example.py
alien_0 = {'color': 'green'}
print(f"The alien is {alien_0['color']}.")

alien_0['color'] = 'yellow'
print(f"The alien is now {alien_0['color']}.")

"""
The alien is green.
The alien is now yellow.
"""
```

A more complex example:
```Python title:example.py
alien_0 = {'x_position': 0, 'y_position': 25, 'speed': 'medium'}
print(f"Original x-position: {alien_0['x_position']}")

# Move the alien to the right.
# Determine how far to move the alien based on its current speed.
if alien_0['speed'] = 'slow':
	x_increment = 1
elif alien_0['speed'] = 'medium':
	x_increment = 2
else:
	x_increment = 3

# The new position is the old position plus the increment
alien_0['x_position'] = alien_0['x_position'] + x_increment

print(f"New x-position: {alien_0['x_position']}")

"""
Original x-position: 0
New x-position: 2
"""
```

#### Removing Key-Value Pairs
```Python title:example.py
alien_0 = {'color': 'green', 'points': 5}
print(alien_0)

del alien_0['points']
print(alien_0)

"""
{'color': 'green', 'points': 5}
{'color': 'green'}
"""
```

**⚠️ Note:** Be aware that the deleted key-value pair is removed permanently.

#### A Dictionary of Similar Objects
```Python title:example.py
favorite_languages = {
	'jen': 'python',
	'sarah': 'c',
	'edward': 'rust',
	'phil': 'python',
}

language = favorite_languages['sarah'].title()
print(f"Sarah's favorite language is {language}.")

"""
Sarah's favorite language is C.
"""
```

#### Using get() to Access Values
```Python title:example.py
alien_0 = {'color', 'green', 'speed': 'slow'}
print(alien_0['points'])

"""
Traceback (most recent call last):
	File "alien_no_points.py", line 2, in <module>
		print(alien_0['points'])
		      ~~~~~~~^^^^^^^^^^
KeyError: 'points'
"""
```

For dictionaries, you can use the `get()` method to set a default value that will be returned if the requested key doesn’t exist:
```Python title:example.py
aline_0 = {'color': 'green', 'speed': 'slow'}

point_value = alien_0.get('points', 'No point value assigned.')
print(point_value)

"""
No point value assigned.
"""
```

If there’s a chance the key you’re asking for might not exist, consider using the `get()` method instead of the square bracket notation.

**Note:** If you leave out the second argument in the call to `get()` and the key doesn’t exist, Python will return the value `None`. The special value `None` means that “no value exists.” This is not a n error: it’s a special value meant to indicate the absence of a value.