### Meta
2024-11-03 11:36
**Tags:** [[python]] [[py_basics]] [[py_classes]]
**Status:** #**completed** 

### Importing Classes
As you add more functionality to your classes, your files can get long, even if you use inheritance and composition properly. In keeping with the overall philosophy of Python, you’ll want to keep your files as uncluttered as possible. To help, Python lets you store classes n modules and then import the classes you need into your main program.

#### Importing a Single Class
```Python title:car.py
"""A class that can be used to represent a car."""\

class Car:
	"""A simple attempt to represent a car."""

	def __init__(self, make, model, year):
		"""Initialize attributes to describe a car."""
		self.make = make
		self.model = model
		self.year = year
		self.odometer_reading = 0

	def get_descriptive_name(self):
	"""Return a neatly formatted descriptive name."""
	long_name = f"{self.year} {self.make} {self.model}"
	return long_name.title()

	def read_odometer(self):
	"""Print a statement showing the car's mileage."""
	print(f"This car has {self.odometer_reading} miles on it.")

	def update_odometer(self, mileage):
	"""
	Set the odometer reading to the given value.
	Reject the change if it attempts to roll the odometer back.
	"""
	if mileage >= self.odometer_reading:
		self.odometer_reading = mileage
	else:
		print("You can't roll back an odometer!")

	def increment_odometer(self, miles):
		"""Add the given amount to the odometer reading."""
		self.odometer_reading += miles
```

Write a docstring at the beginning of each module you create.

```Python title:my_car.py
from car import Car

my new_car = Car('audi', 'a4', 2024)
print(my_new_car.get_descriptive_name())

my_new_car.odometer_reading = 23
my_new_car.read_odometer()

"""
2024 Audi A4
This car has 23 miles on it.
"""
```

#### Storing Multiple Classes in a Module
You can store as many classes as you need in a single module, although every class in a module should be related somehow. The classes `Battery` and `ElectricCar` both help represent cars, so you can add them to the module *car.py*.
```Python title:car.py
"""A set of classes used to represent gas and electric cars."""

class Car:
	--snip--

class Battery:
	"""A simple attempt to model a battery for an electric car."""

	def __init__(self, battery_size=40):
		"""Initialize the battery's attributes."""
		self.battery_size = battery_size

	def describe_battery(self):
		"""Print a statement describing the battery size."""
		print(f"This car has {self.battery_size}-kWh battery.")

	def get_range(self):
		"""Print a statement about the range this battery provides."""
		if self.battery_size == 40:
			range = 150
		elif self.battery_size == 65:
			range = 225

	print(f"This car can go about {range} miles on a full charge.")

class ElectricCar(Car):
	"""Models aspects of a car, specific to electric vehicles."""

	def __init__(self, make, model, year):
		"""
		Initialize attributes of the parent class.
		Then initialize attributes specific to an electric car.
		"""
		super().__init__(make, model, year)
		self.battery = Battery()
```

Now we can create a new file called *my_electric_car.py*, import the `ElectricCar` class, and instantiate it:
```Python title:my_electric_car.py
from car import ElectricCar

my_leaf = ElectricCar('nissan', 'leaf', 2024)
print(my_leaf.get_descriptive_name())
my_leaf.battery.describe_battery()
my_leaf.battery.get_range()

"""
2024
This car has a 40-kWh battery.
This car can go about 150 miles on a full charge.
"""
```

#### Importing Multiple Classes from a Module
```Python title:my_cars.py
from car import Car, ElectricCar

my_mustang = Car('ford', 'mustang', 2024)
print(my_mustang.get_descriptive_name())
my_leaf = ElectricCar('nissan', 'leaf', 2024)
print(my_leaf.get_descriptive_name())

"""
2024 Ford Mustang
2024 Nissan Leaf
"""
```

#### Importing an Entire Module
```Python title:my_cars.py
import car

my_mustang = car.Car('ford', 'mustang', 2024)
print(my_mustang.get_descriptive_name())

my_leaf = car.ElectricCar('nissan', 'leaf', 2024)
print(my_leaf.get_descriptive_name())

"""
2024 Ford Mustang
2024 Nissan Leaf
"""
```

#### Importing all Classes from a Module
```Python title:example.py
from module_name import *
```

This method is not recommended for two reasons.

First, it’s helpful to be able to read the `import` statements at the top of a file and get a clear sense of which classes a program uses. With this approach, this becomes unclear.

This approach can also lead to confusion with names in the file. If you accidentally import class with the same name as something else in your program file, you can create errors that are hard to diagnose.

If you need to import many classes from a module, you’re better off importing the entire module and using the `from module_name import ClassName` syntax.

#### Importing a Module into a Module
Sometimes you’ll want to spread out your classes over several modules to keep any one file from growing too large and avoid storing unrelated classes in the same module. When you store classes in several modules, you may find that a class in one module depends on a class in another module. When this happens, you can import the required class into the first module.
```Python title:electric_car.py
"""A set of classes that can be used to represent electric cars."""

from car import Car

class Battery:
	--snip--

class ElectricCar(Car):
	--snip--
```

```Python title:car.py
"""A class that can be used to represent a car."""

class Car:
	--snip--
```

```Python title:my_cars.py
from car import Car
from electric_car import ElectricCar

my_mustang = Car('ford', 'mustang', 2024)
print(my_mustang.get_descriptive_name())

my_leaf = ElectricCar('nissan', 'leaf', 2024)
print(my_leaf.get_descriptive_name())

"""
2024 Ford Mustang
2024 Nissan Leaf
"""
```

#### Using Aliases
```Python title:example.py
# Import class with alias
from electric_car import ElectricCar as EC

# Import module with alias
import electric_car as ec

"""
...
"""

my_leaf = EC('nissan', 'leaf', 2024)

"""
2024 Nissan Leaf
"""
```