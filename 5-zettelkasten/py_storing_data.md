### Meta
2024-11-05 11:05
**Tags:** [[python]] [[py_basics]] [[py_files_exceptions]]
**Status:** #pending 

### Storing Data
When users close a program, you’ll almost always want to save the information they entered. A simple way to do this involves storing your data using the `json` module.

The `json` module allows you convert simple Python data structures into JSON-formatted strings, and then load the data from the file the next time the program runs. You can also use `json` to share data between different Python programs. Even better, JSON data format is not specific to Python, so you can share data you store in the JSON format with people who work in many other programming language.

#### Using json.dumps() and json.loads()
Let’s write a short program that stores a set of numbers and another program that reads these numbers back into memory. The first program will use `json.dumps()` to store the set of numbers, and the second program will use `json.loads()`.

The `json.dumps` function takes one argument: a piece of data that should be converted to JSON. The function returns a string, which we can then write to a data file:
```Python title:number_writer.py
from pathlib import Path
import json

numbers = [2, 3, 5, 7, 11, 13]

path = Path('numbers.json')
contents = json.dumps(numbers)
path.write_text(contents)

"""
	numbers.json:
[2, 3, 5, 7, 11, 13]
"""
```

Now, we’ll write a separate program that uses `json.loads()` to read the list back into memory:
```Python title:number_reader.py
from pathlib import Path
import json

path = Path('numbers.json')
contents = path.read_text()
numbers = json.loads(contents)

print(numbers)

"""
[2, 3, 5, 7, 11, 13]
"""
```

#### Saving and Reading User-Generated Data
Saving data with `json` is useful when you’re working with user-generated data, because if you don’t store your user’s information somehow, you’ll lose it when the program stops running.

```Python title:remember_me.py
from pathlib import Path
import json

username = input("What's your name? ")

path = Path('username.json')
contents = json.dumps(username)
path.write_text(contents)

print(f"We'll remember you when you come back, {username}!")

"""
What's your name? Eric
We'll remember you when you come back, Eric!
"""
```

Now let’s write a new program that greets a user whose name has already been stored:
```Python title:greet_user.py
from pathlib import Path
import json

path = Path('username.json')
contents = path.read_text()
username = json.loads(contents)

print(f"Welcome back, {username}!")

"""
Welcome back, Eric!
"""
```

We need to combine these two programs into one file. When someone runs *remember_me.py*, we want to retrieve the username from memory if possible; if not, we’ll prompt for a username and store it in *username.json* for next time. We could write a `try-except` block here to respond appropriately if *username.json* doesn’t exist, but instead we’ll use a handy method from the `pathlib` module:

```Python title:remember_me.py
from pathlib import Path
import json

path = Path('username.json')
if path.exists():
	contents = path.read_text()
	username = json.loads(contents)
	print(f"Welcome back, {username}!")
else:
	username = input("What's your name? ")
	contents = json.dumps(username)
	path.write_text(contents)
	print(f"We'll remember when you come back, {username}!")
```

The `exists()` method of `Path` instances returns `True` if a file or folder exists, and `False` otherwise.

#### Refactoring
Often, you’ll reach a point where your code will work, but can be improved by breaking it up into functions with specific tasks. This process is called *refactoring*. Refactoring makes your code cleaner, easier to understand, and easier to extend.

```Python title:remember_me.py
from pathlib import Path
import json

def greet_user():
	"""Greet the user by name."""
	path = Path('username.json')
	if path.exists():
		contents = path.read_text()
		username = json.loads(contents)
		print(f"Welcome back, {username}!")
	else:
		username = input("What's your name? ")
		contents = json.dumps(username)
		path.write_text(contents)
		parint(f"We'll remember you when you come back, {username}!")

greet_user()
```

We’ve refactored into a function, but it performs too many tasks. Let’s break it up even further.

```Python title:remember_me.py
from pathlib import Path
import json

def get_stored_username(path):
	"""Retrieves stored username if available."""
	if path.exists():
		contents = path.read_text()
		username = json.loads(contents)
		return username
	else:
		return None

def greet_user():
	"""Greet user by name."""
	path = Path('username.json')
	username = get_stored_username(path)
	if username:
		print(f"Welcome back, {username}!")
	else:
		username = input("What's your name? ")
		contents = json.dumps(username)
		path.write_text(contents)
		print(f"We'll remember you when you come back, {username}!")

greet(user)
```

We can factor one more block of code out of `greet_user()`. If the username doesn’t exist, we should move the code that prompts for a new username to a function dedicated to that purpose:
```Python title:remember_me.py
from pathlib import Path
import json

def get_stored_username(path):
	"""Retrieves stored username if available."""
	if path.exists():
		contents = path.read_text()
		username = json.loads(contents)
		return username
	else:
		return None

def get_new_username(path):
	"""Prompt for a new username."""
	username = input("What is your name? ")
	contents = json.dumps(username)
	path.write_text(contents)
	return username

def greet_user():
	"""Greet user by name."""
	path = Path('username.json')
	username = get_stored_username(path)
	if username:
		print(f"Welcome back, {username}!")
	else:
		username = get_new_username(path)
		print(f"We'll remember you when you come back, {username}!")

greet()
```
