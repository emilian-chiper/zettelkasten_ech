### Meta
2024-10-30 12:41
**Tags:** [[python]] [[py_basics]] [[py_conditionals]]
**Status:** #completed 

### Conditional Tests
At the heart of every `if` statement is an expression that can be evaluated as either `True` or `False`, and is called a *conditional*. If a condition evaluates to `True`, Python executes the code following the `if` statement. If it evaluates to `False`, Python ignores the code following the `if` statement.

#### Checking for Equality
```Python title:example.py
car = 'bmw' # assignment
print(car == 'bmw') # equality test

"""
True
"""
```

`=` is the assignment operator, while `==` is the equality operator.

#### Ignoring Case when Checking for Equality
```Python title:example.py
car = 'Audi'
print(car == 'audi')

"""
False
"""
```

Testing for equality is case sensitive in Python.

Workaround:
```Python title:example.py
car = 'Audi'
print(car.lower() == 'audi')

"""
True
"""
```

#### Checking for Inequality
Use the inequality operator `!=`.
```Python title:example.py
requested_topping = 'mushrooms'

if requested_topping != 'anchovies':
	print("Hold the anchovies!")

"""
Hold the anchovies!
"""
```

#### Numerical Comparisons
```Python title:example.py
age = 18
print(age == 18)

"""
True
"""

answer = 17
if answer != 42:
	print("That is not the correct answer. Please try again!")

"""
That is not the correct answer. Please try again!
"""
```

Mathematical comparisons:
```Python title:example.py
age = 19
print(age < 21) # True
print(age <= 21) # True
print(age > 21) # False
print(age >= 21) # False
```

#### Checking Multiple Conditions
Sometimes you might need several conditions to be `True` to take action. Other times, you might be satisfied with just one condition being `True`. The keywords `and` and `or` can help you in these situations.

##### Using and to Check Multiple Conditions
```Python title:example.py
age_0 = 22
age_1 = 18
print(age_0 >= 21 and age_1 >= 21) # False

age_1 = 22
print(age_0 >= 21 and age_1 >= 21) # True
```

`and` fails when either condition evaluates to `False`.

You can use parentheses to improve readability (e.g. `(age_0 >= 21) and (age_1 >= 21)`).

##### Using or to Check Multiple Conditions
```Python title:example.py
age_0 = 22
age_1 = 18
print(age_0 >= 21 or age_1 >= 21) # True

age_0 = 18
print(age_0 >= 21 or age_1 >= 21) # False
```

`or` fails only when both conditions evaluate to `False`.

#### Checking Whether a Value is in a List
```Python title:example.py
requested_toppings = ['mushrooms', 'onions', 'pineapple']
print('mushrooms' in requested_toppings) # True
print('pepperoni' in requested_toppings) # False
```

The keyword `in` tells Python to check for the existence of the specified value in the list.

#### Checking Whether a Value is Not in a List
```Python title:example.py
banned_users = ['andrew', 'carolina', 'david']
user = 'marie'

if user not in banned_users:
	print(f"{user.title()}, you can post a response if you wish.")

"""
Marie, you can post a respose if you wish.
"""
```

#### Boolean Expressions
A *Boolean expression* is another name for a conditional test. A *Boolean value* is either `True` or `False`.

Boolean values are often used to keep track of certain conditionts, such as whether a game is running or whether a user can edit certain content on a website:
```Python title:example.py
game_active = True
can_edit = False
```