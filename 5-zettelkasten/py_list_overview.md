### Meta
2024-10-28 21:48
**Tags:** [[python]] [[py_basics]] [[py_lists]]
**Status:** #completed 

### What is a List?
A *list* is a collection of items in a particular order. Can contain any data type.

In Python, square brackets `[]` indicate a list, and individual elements inside are separated by commas.
```Python title:example.py
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles) # ['trek', ..., 'specialized']
```

#### Accessing Elements in a List
Lists are ordered collections. You can access any element by specifying its position, or *index*.
```Python title:example.py
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[0]) # trek
print(bicycles[0].title()) # Trek
```

#### Indexing
Index positions start at `0`.
```Python title:example.py
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[1]) # cannondale
print(bicycles[3]) # specialized
```

To access the last element, you can specify index `-1`
```Python title:example.py
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[-1]) # specialized
```

#### Using Individual Values from a List
```Python title:example.py
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
message = f"My first bicycle was a {bicycle[0].title()}."
print(message) # My first bicycle was a Trek.
```