### Meta
2024-10-29 18:35
**Tags:** [[python]] [[py_basics]] [[py_working_with_lists]]
**Status:** #pending 

### Slicing a List
To make a slice, you specify the index of the first and last elements you want to work with. Python stops one item before the second specified index.
```Python title:example.py
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[0:3]) # ['charles', 'martina', 'michael']
```

You can generate any desired subset:
```Python title:example.py
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[1:4]) # ['martina', 'michael', 'florence']
```

Omitting the first index automatically starts the slice from the beginning of the list:
```Python title:example.py
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[:4]) # ['charles', 'martina', 'michael', 'florence']
```

A similar syntax works if you want to include the end of the list:
```Python title:example.py
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[2:]) # ['michael', 'florence', 'eli']
```

A negative index returns an element a certain distance from the end of the list:
```Python title:example.py
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[-3:]) # ['michael', 'florence', 'eli']
```

**Note:** You can include a third value in the brackets, indicating a `step`.

### Looping Through a Slice
```Python title:example.py
players = ['charles', 'martina', 'michael', 'florence', 'eli']

print("Here are the first three players on my team:")
for player in players[:3]:
	print(player.title())

"""
Here are the first three players on my team:
Charles
Martina
Michael
"""
```

### Copying a List
To copy a list, you can make a slice that includes the entire original list by omitting the first and second index.
```Python title:example.py
my_foods = ['pizza', 'falafel', 'carrot cake']
friends_foods = my_foods[:]

print("My favorite foods are:")
print(my_foods)

print("\nMy friend's favorite foods are:")
print(friend_foods)

"""
My favorite foods are:
['pizza', 'falafel', 'carrot cake']

My friend's favorite foods are:
['pizza', 'falafel', 'carrot cake']
"""
```

Proof:
```Python title:example.py
my_foods = ['pizza', 'falafel', 'carrot cake']
friend_foods = my_foods[:]

my_foods.append('cannoli')
fiend_foods.append('ice cream')

print("My favorite foods are:")
print(my_foods)

print("\nMy friend's favorite foods are:")
print(friend_foods)

"""
My favorite foods are:
['pizza', 'falafel', 'carrot cake', 'cannoli']

My friend's favorite foods are:
['pizza', 'falafel', 'carrot cake', 'ice cream']
"""
```

If we had simply set `friend_foods` equal to `my_foods`, we would not produce two separate lists, but instead copied by reference to `my_foods` into `friend_foods`. Any change to `friend_foods` would be reflected in `my_foods`, and vice-versa.