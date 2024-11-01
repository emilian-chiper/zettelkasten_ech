### Meta
2024-10-28 18:16
**Tags:** [[python]] [[py_basics]] [[py_variables_simple_data_types]]
**Status:** #completed 

### Strings
A *string* is a series of characters. Anything inside quotes is considered a string in Python. You can use single or double quotes.
```Python title:example.py
"This is a string."
'This is also a string.'
```

This flexibility allows you to use quotes and apostrophes within your strings:
```Python title:example.py
'I told my friend, "Python is my favorite language!"'
"Tha langauge 'Python' is named after Monthy Python, not the snake."
"One of Python's strengths is its diverse and supportive community."
```

#### Changing Case in a String with Methods
```Python title:example.py
name = "ada lovelace"
print(name.title()) # output: Ada Lovelace
print(name.upper()) # output: ADA LOVELACE
print(name.lower()) # output: ada lovelace
```

#### Using Variables in Strings
```Python title:example.py
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
print(full_name) # output: ada lovelace
```

The expression on line 3 is that of an assignment to an *f-string*. The *f* is for *format*, because Python formats the string by replacing the name of any variable in braces with its value.

You can use f-strings to compose complete messages using the information associated with a variable:
```Python title:example.py
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
print(f"Hello, {full_name.title()}!") # Hello, Ada Lovelace!
```

You can also use f-strings to compose a message, and then assign the entire message to a variable:
```Python title:example.py
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
message = f"Hello, {full_name.title()}!"
print(message) # output: Hello, Ada Lovelace!
```

#### Adding Whitespace to Strings with Tabs or Newlines
*Whitespace* refers to any nonprinting characters, such as spaces, tabs, and end-of-line symbols. You can organize your output with this feature.
```BASH title:example.sh
>>> print("Python")
Python
>>> print("\tPython")
	Python
```

You can use `\t` for tabs and `\n` for newline. Can be combined.

#### Stripping Whitespace
`str.rstrip()` removes whitespace from the right side of a string.
`str.lstrip()` removes whitespace from the left side of a string.
`str.strip()` removes whitespace from both sides of a string.

In the real world, these stripping functions are most often used to clean up user input before it’s stored in a program.
#### Removing Prefixes
When working with strings, it’s a common task to remove a prefix, such as in the case of an URL (i.e., `https://`).
```BASH title:example.sh
>>> nostarch_url = "https://nostarch.com"
>>> nostarch_url.removeprefix('https://')
```

Like the methods for removing whitespace, `str.removeprefix()` leaves the original string unchanged. If you want to store the new value with the prefix removed, reassign it to the original variable or assign it to a new one.

#### Avoiding Syntax Errors with Strings
A *syntax error* occurs when Python doesn’t recognize a section of your program as valid Python code, e.g., using an apostrophe inside single quotes. Python interprets everything between the first single quote and the apostrophe as a string, and parses the second part afterwards, which it cannot do successfully. Ergo, the error. To avoid that, use double quotes.