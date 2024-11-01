### Meta
2024-10-28 21:30
**Tags:** [[python]] [[py_basics]] [[py_variables_simple_data_types]]
**Status:** #completed 

### Integers
```Python title:example.py
2 + 3 # addition
3 - 2 # subtraction
2 * 3 # multiplication
3 / 2 # division
3 ** 2 # exponentiation
```

Python supports the order of operations. You can modify it with parentheses
```Python title:example.py
2 + 3 * 4 # 14
(2 + 3) * 4 # 20
```

### Floats
Python calls any number with a decimal point a *float*. Floats support the same operations as integers.

You can sometimes get an arbitrary number of decimal places in your answer:
```Python title:example.py
0.2 + 0.1 # 0.30000000000000004
```

This happens due to the difficulty of translating decimal fractions into the binary system and vice-versa.

### Integers and Floats
When you divide any two numbers, even if they are integers, the result will always be a float. Same goes for mixing integers and floats.

### Underscores in Numbers
Underscores `_` serve as a visual aid when writing large numbers. The Python interpreter ignores them.

### Multiple Assignment
```Python title:example.py
x, y, z = 0, 0, 0
```

### Constants
A *constant* is a variable whose value stays the same throughout the life of a program. Python doesn’t have any built-in constant types, but Python programmers use all capital letters to indicate a variable should be treated as a constant and never be changed.
```Python title:example.py
MAX_CONNECTIONS = 5000
```