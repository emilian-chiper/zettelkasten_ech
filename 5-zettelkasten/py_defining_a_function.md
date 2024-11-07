### Meta
2024-11-01 11:47
**Tags:** [[python]] [[py_basics]] [[py_functions]]
**Status:** #completed 

### Defining Functions
A *function* is a named block of code designed to do one specific job. When you want to perform a particular task that you’ve defined in a function, you *call* the function responsible for it.

```Python title:example.py
def greet_user():
"""Display a simple greeting."""
	print("Hello!")

greet_user() # Hello!
```

The first line uses the keyword `def` to inform Python that you’re defining a function. This is the *function definition*, which tells Python the name of the function and, if applicable, what kind of information the function needs to do its job. The parentheses hold that information. They are required, even if empty. The definition ends in a colon `:`.

Any indented lines that follow the function definition make up the *body* of the function. The text on the second line is a comment called a *docstring*, which describes what a function does. When Python generates documentation for the functions in your programs, it looks for a string immediately after the function’s definition. These strings are usually enclosed in triple quotes, which lets you write multiple lines.

When you want to use this function, you call it. A *function call* tells Python to execute the code in the function. To *call* a function, you write the name of the function, followed by any necessary information in parentheses.

### Passing Information to a Function
```Python title:example.py
def greet_user(username):
	"""Display a simple greeting."""
	print(f"Hello, {username.title()}")

greet_user('waltuh') # Hello, Waltuh!
```

### Arguments and Parameters
The variable `username` in the definition of `greet_user()` above is an example of a *parameter*, a piece of info the function requires to do its job. The value `'waltuh'` passed to the function in its call is an *argument*.