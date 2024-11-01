### Meta
2024-10-29 18:12
**Tags:** [[python]] [[py_basics]] [[py_working_with_lists]]
**Status:** #pending 

### Using the range() Function
Python’s `range()` function generates a series of numbers.
```Python title:example.py
for value in range(1, 5):
	print(value)

"""
	Output:
1
2
3
4
"""
```

`range()` prints numbers `1` through `4`. This is another result of the off-by-one behavior frequently seen in programming languages.

`range()` causes Python to start counting at the first value provided, and it stops when it reaches the second, not included.

You can also pass `range()` only one argument, and it starts counting from `0`.

### Using range() to Make a List of Numbers
```Python title:example.py
numbers = list(range(1, 6))
print(numbers) # [1, 2, 3, 4, 5]
```

We can also tell Python to skip numbers with a third argument, a `step`.
```Python title:example.py
even_numbers = list(range(2, 11, 2))
print(even_numbers) # [2, 4, 6, 8, 10]
```

`range()` adds to repeatedly until it reaches or passes the `end` value.

A more complex example, involving the squares of the first 10 numbers of $Z^+$ (the set of positive integers).
```Python title:example.py
squares = []
for value in range(1, 11):
	square = value ** 2
	squares.append(square)

print(squares) # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

More concisely:
```Python title:example.py
squares = []
for value in range(1, 11):
	squares.append(value**2)

print(squares)
```

### Simple Statistics with a List of Numbers
```Python title:example.py
digits = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
print(min(digits)) # 0
print(max(digits)) # 9
print(sum(digits)) # 45
```

### List Comprehensions
A *list comprehension* allows you to generate a list in just one line of code. It combines the `for` loop and the creation of new elements in one line, and automatically appends each new element.
```Python title:example.py
squares = [value**2 for value in range(1, 11)];
print(squares) # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```