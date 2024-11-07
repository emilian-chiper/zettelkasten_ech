### Meta
2024-11-02 21:33
**Tags:** [[python]] [[py_basics]] [[py_classes]]
**Status:** #completed 

### Inheritance
You don’t always have to start from scratch when writing a class. If the class you’re writing is a specialized version of another class you wrote, you can use *inheritance*. When one class *inherits* from another, it takes on the attributes and methods of the first class. The original class is called the *parent class*, and the new class is the *child class*. The child class can inherit any or all of the attributes and methods of its parent class, but it’s also free to define new attributes and methods of its own.

#### The `__init__()` Method for a Child Class
When writing a new class based on an existing class, you’ll often want to call the `__init__()` method from the parent class. This will initialize any attributes that were defined in the parent `__init__()` method and make them available in the child class.

```Python title:example.py
class Car:
	"""A simple representation of a car."""

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
		"""Print a statemetn showing the car's mileage."""
		print(f"This car has {self.odometer_reading} miles on it.")

	def update_odometer(self, mileage):
		"""Set the odometer reading to the given value."""
		if mileage >= self.odometer_reading:
			self.odometer_reading = mileage
		else:
			print("You can't roll back an odometer!")

	def increment_odometer(self, miles):
		"""Add the given amount to the odometer reading."""
		self.odometer_reading += miles

class ElectricCar(Car):
	"""Represents aspects of a car, specific to electric vehicles."""
	def __init__(self, make, model, year):
		"""Initialize attributes of the parent class."""
		super().__init__(make, model, year)

my_leaf = ElectricCar('nissan', 'leaf', 2024)
print(my_leaf.get_descriptive_name())

"""
2024 Nissan Leaf
"""
```

When you create a child class, the parent class must be part of the current file and must appear before the child class in the file.

The name of the parent class must be included in parentheses in the definition of a child class.

The `super()` function allows us to call a method from the parent class. The name *super* comes from a convention of calling the parent class a *superclass* and the child class a *subclass*.

#### Defining Attributes and Methods for the Child Class
```Python title:example.py
class Car:
	--snip--

class ElectricCar(Car):
	"""Represent aspects of a car, specific to electric vehicles."""

	def __init__(self, make, model, year):
		"""
		Initialize attributes of the parent class.
		Then initialize attributes specific to an electric car.
		"""
		super().__init__(make, model, year)
		self.battery_size = 40

	def describe_battery(self):
		"""Print a statemetn describing battery size."""
		print(f"This car has a {self.battery_size}-kWh battery.")

my_leaf = ElectricCar('nissan', 'leaf', 2024)
print(my_leaf.get_descriptive_name())
my_leaf.describe_battery()

"""
2024 Nissan Leaf
This car has a 40-kWh battery.
"""
```

#### Overriding Methods from the Parent Class
To do this, you define a method in the child class with the same name as the method you want to override in the parent class.

e.g., the `Car` class has a method called `fill_gas_tank()`, which is meaningless for electric cars.
```Python title:example.py
class ElectricCar(Car):
	--snip--

	def fill_gas_tank(self):
		"""Electric cars don't have gas tanks."""
		print("This car doesn't have a gas tank!")
```

#### Instances as Attributes
You can break your large classes into smaller classes that work together; this approach is called *composition*.

For example, if we keep adding detail to the `ElectricCar` class, we might notice that we’re adding many attributes and methods specific to the car’s battery. When we realize this, we can stop and move those attributes and methods to a separate class called `Battery`. Then we can use `Battery` instance as an attribute in the `ElectricCar` class:
```Python title:example.py
class Car:
	--snip--

class Battery:
	"""A simple model of a battery for an electri car."""

	def __init__(self, battery_size=40):
		"""Initialize the battery's attributes."""
		self.battery_size = battery_size

	def describe_battery(self):
		"""Print a statement describing the battery size."""
		print(f"This car has a {self.battery_size}-kW battery.")

	def get_range(self):
		"""Print a statemetn about the range this battery provides."""
		if self.battery_size == 40:
			range = 150
		elif self.battery_size == 65:
			range = 225

		print(f"This car can go about {range} miles on a full charge.")

class ElectricCar(Car):
	"""Represent aspects of a car, specific to electric vehicles."""

	def __init__(self, make, model, year):
		"""
		Initialize attributes of the parent class.
		Then initialize attribtues specific to an electric car.
		"""
		super().__init__(make, model, year)
		self.battery = Battery()

my_leaf = ElectricCar('nissan', 'leaf', 2024)
print(my_leaf.get_descriptive_name())
my_leaf.battery.describe_battery()
my_leaf.battery.get_range()

"""
2024 Nissan Leaf
This car has a 40-kWh battery.
This car can go about 150 miles on a full charge.
"""
```