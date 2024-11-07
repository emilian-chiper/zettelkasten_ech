### Meta
2024-11-01 12:03
**Tags:** [[python]] [[py_basics]] [[py_functions]]
**Status:** #completed 

### Positional Arguments
When you call a function, Python must match each argument in the function call with a parameter in the function definition. The simplest way to do this is based on the order of the arguments provided. Values matched in this way are called *positional arguments*.

```Python title:example.py
def describe_pet(animal_type, pet_name):
	"""Display information about a pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_types}'s name is {pet_name.title()}.")

describe_pet('hamster', 'harry')

"""
I have a hamster.
My hamster's name is Harry.
"""
```

#### Multiple Function Calls
```Python title:example.py
def describe_pet(animal_type, pet_name):
	"""Display information about a pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_types}'s name is {pet_name.title()}.")

describe_pet('hamster', 'harry')
describe_pet('dog', 'brandon')

"""
I have a hasmter.
My hamster's name is Harry.

I have a dog.
My dog's name is Brandon.
"""
```

#### Order Matters in Positional Arguments
```Python title:example.py
def describe_pet(animal_type, pet_name):
	"""Display information about a pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_types}'s name is {pet_name.title()}.")

describe_pet('harry', 'hamster')

"""
I have a harry.
My harry's name is Hamster.
"""
```

### Keyword Arguments
A *keyword argument* is a name-value pair that you pass to a function. You directly associate the name and the value within the argument, so when you pass the argument to the function, there’s no confusion.
```Python title:example.py
def describe_pet(animal_type, pet_name):
	"""Display information about a pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_types}'s name is {pet_name.title()}.")

describe_pet(pet_name='harry', animal_type='hamster')

"""
I have a hamster.
My hamster's name is Harry.
"""
```

### Default Values
When defining a function, you can define a *default value* for each parameter. If an argument for a parameter is provided in the function call, Python uses the argument value. If not, it uses the default value.

```Python title:example.py
def describe_pet(pet_name, animal_type='dog')
	"""Display information abouta pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_type}'s name is {pet_name.title()}.")

describe_pet(pet_name="brandon")
# describe_pet('brandon') works too
# describe_pet(pet_name='harry', animal_type='hamster') overrides the default parameters

"""
I have a dog.
My dog's name is Brandon.
"""
```

**Note:** When using default values, any parameter with a default value must be listed after all the parameters that DON’T have one. This allows Python to continue interpreting positional arguments correctly.

### Equivalent Function Calls
Let’s say we have:
```Python title:example.py
def describe_pet(pet_name, animal_type='dog'):
	""" ---snip--- """

# All of the function calls bellow are valid
describe_pet('willie')
describe_pet(pet_name='willie')

describe_pet('harry', 'hamster')
describe_pet(pet_name='harry', animal_type='hamster')
describe_pet(animal_type='hamster', pet_name='harry')
```

### Avoiding Argument Errors
```Python title:example.py
def describe_pet(animal_type, pet_name):
	"""Display information about a pet."""
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_types}'s name is {pet_name.title()}.")

describe_pet()

"""
Traceback (most recent call last):
  File "pets.py", line 6, in <module>
    describe_pet()
    ^^^^^^^^^^^^^^
TypeError: describe_pet() missing 2 required positional arguments:
    'animal_type' and 'pet_name'
"""
```