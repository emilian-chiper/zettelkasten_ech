### Meta
2024-11-02 17:59
**Tags:** [[python]] [[py_basics]] [[py_classes]]
**Status:** #pending 

### Creating and Using a Class
*Classes* are blueprints. *Objects* are *instances* of classes, made through a process called *instantiation*. Together, these constitute the working elements of *object-oriented programming* or *OOP*.

#### Creating the Dog Class
```Python title:example.py
class Dog:
	"""A simple attempt to model a dog."""

	def __init__(self, name, age):
		"""Initialize name and age attributes."""
		self.name = name
		self.age = age

	def sit(self):
		"""Simulate a dog sitting in response to a command."""
		print(f"{self.name} is now sitting.")

	def roll_over(self):
		"""Simulate rolling over in response to a command."""
		print(f"{self.name} rolled over!")
```

By convention, capitalized names refer to classes in Python. There are no parentheses in the class definition because we’re creating this class from scratch. We then write a docstring describing what this class does.

##### The `__init__()` Method
A function that’s part of a class is a *method*.

The `__init__()` method is a special method that Python runs automatically whenever we create a new instance based on the `Dog` class. This method has two leading underscores and two trailing underscores, a convention that helps Python’s default method names from conflicting with your method names. If you use just one underscore on each  side, the method won’t be called automatically when you use your class, which can cause errors.

We define the `__init__()` method to have three parameters: `self`, `name`, and `age`.

The `self` parameter is required in the method definition and it must come first, before the other parameters. It must be included in the definition because when Python calls this method later (to create an instance of `Dog`), the method call will automatically pass the `self` argument. Every method call associated with an instance automatically passes `self`, which is a reference to the instance itself; it gives the individual instance access to the parameters and methods in the class.

The two variables defined in the body of the `__init__()` method each have the prefix `self`.  Any variable prefixed with `self` is available to every method in the class, and we’ll also be able to access these variables through any instance created from the class. The line `self.name = name` takes the value associated with the parameter `name` and assigns it to the variable `name`, which is then attached to the instance being created. The same process happens with `self.age = age`. Variables that are accessible through instances like this are called *attributes*.

The `Dog` class has two other method defined: `sit()` and `roll_over()`. Because these methods don’t need additional information to run, we just define them to have one parameter, `self()`. The instances we create later will have access to these methods.

##### Making an Instance of a Class
```Python title:example.py
"""
class Dog:
	--snip--
"""

my_dog = Dog('Willie', 6)

print(f"My dog's name is {my_dog.name}.")
print(f"My dog is {my_dog.age} years old.")

"""
My dog's name is Willie.
My dog is 6 years old.
"""
```

###### Accessing Attributes
To access the attributes of an instance, you use the dot notation.
```Python title:example.py
my_dog.name
```

###### Calling Methods
```Python title:example.py
"""
class Dog:
	--snip--
"""

my_Dog = Dog('Willie', 6)
my_dog.sit()
my_dog.roll_over()

"""
Willie is now sitting.
Willie rolled over!
"""
```

###### Creating Multiple Intances
```Python title:example.py
"""
class Dog:
	--snip--
"""

my_dog = Dog('Willie', 6)
your_dog = Dog('Lucy', 3)

print(f"My dog's name is {my_dog.name}.")
print(f"My dog is {my_dog.age} years old.")
my_dog.sit()

print(f"\nYour dog's name is {your_dog.name}.")
print(f"Your dog is {your_dog.age} years old.")
your_dog.sit()

"""
My dog's name is Willie.
My dog is 6 years old.
Willie is now sitting.

Your dog's name is Lucy.
Your dog is 3 years old.
Lucy is now sitting.
"""
```