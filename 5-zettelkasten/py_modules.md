### Meta
2024-11-02 13:05
**Tags:** [[python]] [[py_basics]] [[py_functions]]
**Status:** #completed 

### Importing an Entire Module
A *module* is a file ending in *.py* that contains code you want to import into your program.

```Python title:pizza.py
def make_pizza(size, *toppings):
	"""Summarize the pizza we are about to make."""
	print(f"\nMaking a {size}-inch pizza with the following toppings:")
	for topping in toppings:
		print(f"- {topping}")
```

In the same directory as *pizza.py*, we create a new file called *making_pizzas.py*:
```Python title:making_pizzas.py
import pizza

pizza.make_pizza(16, 'pepperoni')
pizza.make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')

"""
Making a 16-inch pizza with the following toppings:
- pepperoni

Making a 12-inch pizza with the following toppings:
- mushrooms
- greeen peppers
- extra cheese
"""
```

If you use this kind of `import` statement to import an entire module, use the following format to use the functions inside the module:
```Python title:example.py
module_name.function_name()
```

### Importing Specific Functions
Syntax:
```Python title:example.py
form module_name import function_0, function_1, function_2
```

For example:
```Python title:example.py
from pizza import make_pizza

make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms, 'green peppers', 'extra cheese')
```

### Using as to Give a Function an Alias
Syntax:
```Python title:example.py
from module_name import function_name as alias
```

Example:
```Python title:example.py
from pizza import make_pizza as mp

mp(16,'pepperoni')
```

### Importing All Functions in a Module
Syntax:
```Python title:example.py
from module_name import *
```

Example:
```Python title:example.py
from pizza import *

make_pizza(16, 'pepperoni')
```