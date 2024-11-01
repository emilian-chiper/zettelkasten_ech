### Meta
2024-10-28 13:19
**Tags:** [[python]] [[py_basics]] [[py_variables_simple_data_types]]
**Status:** #pending 

### Variables
```Python title:hello_world_vars.py
message = "Hello Python world!"
print(message)
```

This produces the same output as the previous version.

We’ve added a *variable* named `message`. Every variable is connected to a `value`, which is the information associated with a variable.

Expanding the example:
```Python title:hello_world_vars.py
message = "Hello Python world!"
print(message)

message = "Hello Python Crash Course world!"
print(message)
```

This produces two lines of output:
```BASH title:output.sh
Hello Python world!
Hello Python Crash Course world!
```

#### Naming and Using Variables
- Variable names can contain only letters, numbers, and underscores. They can start with a letter or underscore, *never* with a number.
- Spaces are not allowed in variable names, but underscores can be used to separate words.
- Avoid using Python keywords and function names as variable names.
- Variable names should be short but descriptive.
- Be careful when using `l` and `O`, as they can be confused with `1` and `0`, respectively.

#### Avoiding Name Errors when Using Variables
Typos cause errors:
```Python title:error.py
message = "Hello world!"
print(mesage)
```

The above snippet will cause a `NameError`.

The interpreter provides a traceback when a program cannot run successfully. A *traceback* is a record of where the interpreter ran into trouble when trying to execute your code.

The Python interpreter doesn’t spellcheck your code, but it does ensure that variable names are spelled consistently.

#### Variables are Labels
Think of them as labels (identifiers) you can assign to values. You can also say that a variable references a certain value.