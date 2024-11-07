### Meta
2024-11-02 13:19
**Tags:** [[python]] [[py_basics]] [[py_functions]]
**Status:** #completed 

### Styling Functions
Use descriptive names, made of lowercase letters and underscores (applies to module names as well).

Every function should have a comment explaining concisely what it does. The comment should appear immediately after the function definition and use the docstring format.

If you specify the default value for a parameter, no spaces should be used on either side of the equal sign:
```Python title:example.py
def function_name(param_0, param_1='default value')
```

The same applies to keyword arguments used in function call:
```Python title:example.py
function_name(value_0, param_1='value')
```

Limit lines of code to 79 characters. If a set of parameters causes a function’s definition to be longer, press ENTER after the opening parenthesis on the definition line. On the next line, press the TAB twice to separate the list of arguments from the body of the function, which will only be indented one level.
```Python title:example.py
def function name(
		param_0, param_1, param_2,
		param_3, param_4, param_5):
	function body...
)
```

If your program or module has more than one function, you can separate each by two blank lines to make it easier to see where one function ends and the next one begins.

All `import` statements should be written at the beginning of the file. The only exception is if you use comments at the beginning of your file to describe the overall program.