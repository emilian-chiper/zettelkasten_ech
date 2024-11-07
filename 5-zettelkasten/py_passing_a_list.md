### Meta
2024-11-01 21:32
**Tags:** [[python]] [[py_basics]] [[py_functions]]
**Status:** #completed 

### Passing a List
```Python title:example.py
def greet_users(names):
	"""Print a simple greeting to each user in the list"""
	for name in names:
		msg = f"Hello, {name.title()}!"
		print(msg)

usernames = ['hanna', 'ty', 'margot']
greet_users(usernames)

"""
Hello, Hannah!
Hello, Ty!
Hello, Margot!
"""
```

#### Modifying a List in a Function
```Python title:example.py
unprinted_designs = ['phone case', 'robot pendant', 'dodecahedron']
completed_models = []

while unprinted_settings:
	current_design = unprinted_designs.pop()
	print(f"Printing model: {current_design}")
	completed_models.append(current_design)

print("\nThe following models have been printed:")
for completed_model in completed_models:
	print(completed_model)

"""
Printing model: dodecahedron
Printing model: robot pendant
Printing model: phone case

The following models have been printed:
dodecahedron
robot pendant
phone case
"""
```

We can refactor this code by writing two functions, each with its own task:
```Python title:example.py
def print_models(unprinted_designs, completed_models):
	"""
	Simulate printing each design, until none are left.
	Move each design to completed_models after printing.
	"""
	while unprinted_designs:
		current_design = unprinted_designs.pop()
		print(f"Printing model: {current_design}")
		completed_models.append(current_design)

def show_completed_models(completed_models):
	"""Show all the models that were printed."""
	print("\nThe following models have been printed:")
	for completed_model in completed_models:
		print(completed_model)

unprinted_designs = ['phone case', 'robot pendant', 'dodecahedron']
completed_models = []

print_models(unprinted_designs, completed_models)
show_completed_models(compelted_models)
```

The output is the same as in the previous iteration. This example also demonstrates the idea that every function should have one specific job. The first function prints each design, and the second displays the completed models.

#### Preventing a Function from Modifying a List
```Python title:example.py
function_name(list_name[:])
```

In the previous example, this would be:
```Python title:example.py
print_models(unprinted_designs[:], completed_models)
```