### Meta
2024-10-29 12:44
**Tags:** [[python]] [[py_basics]] [[py_lists]]
**Status:** #pending 

### Organizing a List
Often, lists will be created in an unpredictable order, because you can’t always control the order in which users provide their data. Sometimes you’ll want to preserve the original order of your list, and other times you’ll want to change the original order.

#### Sorting a List Permanently with the sort() Method
The `sort()` method changes the order of the list permanently.

```Python title:example.py
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort()
print(cars) # ['audi', 'bmw', 'subaru', 'toyota']
```

You can also sort in reverse-alphabetical order by passing the argument `reverse=True` to the `sort()` method.

```Python title:example.py
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort(reverse=True)
print(cars) # ['toyota', 'subaru', 'bmw', 'audi']
```

#### Sorting a List Temporarily with the sorted() Function
To avoid mutating the original list, but present it in sorted order, you can use the `sorted()` function.

```Python title:example.py
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(cars) # ['bmw', 'audi', 'toyota', 'subaru']
print(sorted(cars)) # ['audi', 'bmw', 'subaru', 'toyota']
print(cars) # ['bmw', 'audi', 'toyota', 'subaru']
```

The `sorted()` function can also accept a `reverse=True` argument.

**Note:** Sorting a list alphabetically is a bit more complicated when all the values are not lowercase.

#### Printing a List in Reverse Order
To reverse the original order of a list, you can use the `reverse()` method.

```Python title:example.py
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(cars) # ['bmw', 'audi', 'toyota', 'subaru']

cars.reverse()
print(cars) # ['subaru', 'toyota', 'audi', 'bmw']
```

`reverse()` simply reverses the order of the list. It mutates the original list.

#### Finding the Length of a List
You can achieve that with the `len()` function.

```Python title:example.py
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(len(cars)) # 4
```

**Note:** Python counts the items in a list starting with one, so you shouldn’t run into any off-by-one errors when determining the length of a list.