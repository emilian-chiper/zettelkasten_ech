### Meta
2024-10-29 20:33
**Tags:** [[python]] [[py_basics]] [[py_working_with_lists]]
**Status:** #pending 

### Tuples
Sometimes you’ll want to create a list of items that cannot change. Python refers to values that cannot change as *immutable*, and an immutable list is called a *tuple*.

#### Defining a Tuple
```Python title:example.py
dimensions = (200, 50)
print(dimensions[0]) # 200
print(dimensions[1]) # 50
```

Attempting to change an item in a tuple produces an error:
```Python title:example.py
dimensions = (200, 50)
dimensions[0] = 250

"""
Traceback (most recent call last):
  File "dimensions.py", line 2, in <module>
    dimensions[0] = 250
TypeError: 'tuple' object does not support item assignment
"""
```

**Note:** Tuples are technically defined by the presence of a comma; the parentheses make them look neater and more readable. If you want to define a tuple with one element, you must include a trailing comma:
```Python title:example.py
my_t = (3,)
```

#### Looping Through All Values in a Tuple
```Python title:example.py
dimensions = (200, 50)
for dimension in dimensions:
	print(dimension)

"""
200
50
"""
```

### Writing Over a Tuple
Although you can’t modify a tuple, you can assign a new value to a variable that represents a tuple.

```Python title:example.py
dimensions = (200, 50)
print("Original dimensions:")
for dimension in dimensions:
	print(dimension)

dimensions = (400, 100)
print("\nModified dimensions:")
for dimension in dimensions:
print(dimension)

"""
Original dimensions:
200
50

Modified dimensions:
400
100
"""
```