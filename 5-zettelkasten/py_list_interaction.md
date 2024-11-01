### Meta
2024-10-29 08:33
**Tags:** [[python]] [[py_basics]] [[py_lists]]
**Status:** #pending 

### Modifying, Adding, and Removing Elements
Most lists you create will be *dynamic*, meaning you’ll build a list and then add and remove elements from it as your program runs its course.

#### Modifying Elements in a List
The syntax is similar to the one used for accessing an element.
```Python title:example.py
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles) # ['honda', 'yamaha', 'suzuki']

motorcycles[0] = 'ducati'
print(motorcycles) = ['ducati', 'yamaha', 'suzuki']
```

#### Adding Elements to a list
##### Appending Elements to the End of the List
```Python title:example.py
motorcycles = []

motorcycles.append('honda')
motorcycles.append('yamaha')
motorcycles.append('suzuki')

print(motorcycles) # ['honda', 'yamaha', 'suzuki']
```

##### Inserting Elements into a List
```Python title:example.py
motorcycles = ['honda', 'yamaha', 'suzuki']

motorcycles.insert(0, 'ducati')
print(motorcycles) # ['ducati', 'honda', 'yamaha', 'suzuki']
```

#### Removing an Element from a List
##### Removing an item Using the del Statement
```Python title:example.py
motorcycles = ['honda', 'yamaha', 'suzuki']

del motorcycles[1]
print(motorcycles) # ['honda', 'suzuki']
```

You can no longer access the value that was removed from the list after the `del` statement is used.

##### Removing an Item Using the pop() Method
The `pop()` removes the last item in a list, but it lets you work with that item after removing it.

```Python title:example.py
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles) # ['honda', 'yamaha', 'suzuki']

popped_motorcycle = motorcycles.pop()
print(motorcycles) # ['honda', 'yamaha']
print(popped_motorcycle) # suzuki
```

##### Popping Items from Any Position in a List
```Python title:example.py
motorcycles = ['honda', 'yamaha', 'suzuki']

first_owned = motorcycles.pop()
print(f"The first motorcycle I owned was a {first_owned.title()}")
```

##### Removing an Item by Value
If you know the value of the item you want to remove, you can use the `remove()` method.

```Python title:example.py
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati]
print(motorcycles) # ['honda', 'yamaha', 'suzuki', 'ducati']

motorcycles.remove('ducati')
print(motorcycles) # ['honda', 'yamaha', 'suzuki']
```

You can also use the `remove()` method to work with a value that’s being removed from a list.

```Python title:example.py
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati']

too_expensive = 'ducati'
motorcycles.remove(too_expensive)
print(motorcycles) # ['honda', 'yamaha', 'suzuki']
print(f"\nA {too_expensive.title() is too expensive for me.})
```

**Note:**  The`remove()` method deletes only the first occurrence of the value you specify. If there’s a possibility the value appears more than once in the list, you’ll need to use a loop to ensure all occurrences of the value are removed.