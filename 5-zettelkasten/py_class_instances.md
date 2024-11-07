### Meta
2024-11-02 19:47
**Tags:** [[python]] [[py_basics]] [[py_classes]]
**Status:** #completed 

### Working with Classes and Instances
Once you write a class, you’ll spend most of your time working with instances created from that class. One of the first tasks you’ll want to do is modify the attributes associated with a particular instances. You can modify the attributes of an instance directly or write methods that update attributes in specific ways.

#### The Car Class
```Python title:example.py
class Car:
	"""A simple attempt to represent a car."""

	def __init__(self, make, model, year):
		"""Initialize attributes to describe a car."""
		self.make = make
		self.model = model
		self.year = year

	def get_descriptive_name(self):
		"""Return a neatly formatted descriptive name."""
		long_name = f"{self.year} {self.make} {self.model}"
		return long_name.title()

my_new_car = Car('audi', 'a4, 2024)
print(my_new_car.get_descriptive_name())

"""
2024 Audi A4
"""
```

#### Setting a Default Value for an Attribute
When an instance is created, attributes can be defined without being passed in as a parameter. These attributes can be defined in the `__init__()` method, where they are assigned a default value.

```Python title:example.py
class Car:

	def __init__(self, make, model, year):
		"""Initialize attributes to describe a car."""
		self.make = make
		self.model = model
		self.year = year
		self.odometer_reading = 0

	def get_descriptive_name(self):
		# --snip--

	def read_odometer(self):
		"""Print a statement showing the car's mileage."""
		print(f"This car har {self.odometer_reading} miles on it.")

my_new_car = Car('audi', 'a4', 2024)
print(my_new_car.get_descriptive_name())
my_new_car.read_odometer()

"""
2024 Audi A4
This car has 0 miles on it.
"""
```

#### Modifying Attribute Values
You can change an attribute’s value in three ways: you can change the value directly through an instance, set the value through a method, or increment the value (add a certain amount of it) through a method.

##### Modifying an Attribute’s Value Directly
```Python title:example.py
class Car:
	--snip--

my_new_car = Car('audi', 'a4', 2024)
print(my_new_car.get_descriptive_name())

my_new_car.odometer_reading = 23
my_new_car.read_odometer()

"""
2024 Audi A4
This car has 23 miles on it.
"""
```

##### Modifying an Attribute’s Value Through a Method
```Python title:example.py
class Car:
	--snip--

	def update_odometer(self, mileage):
		"""Set the odometer reading to the given value."""
		self.odometer_reading = mileage

my_new_car = Car('audi', 'a4', 2024)
print(my_new_car.get_descriptive_name())

my_new_car.update_odometer(23)
my_new_car.read_odometer()

"""
2024 Audi A4
This car has 23 miles on it.
"""
```

We can extend the method `update_odometer()` to do additional work every time the odometer reading is modified.
```Python title:example.py
class Car:
	--snip--

	def update_odometer(self, mileage):
		"""
		Set the odometer reading the given value.
		Reject the change if it attempts to roll the odometer back.
		"""
		if mileage >= self.odometer_reading:
			self.odometer_reading = mileage
		else:
			print("You can't roll back an odometer!")
```

##### Incrementing an Attribute’s Value Through a Method
Sometimes you’ll want to increment an attribute’s value by a certain amount, rather than set an entirely new value.
```Python title:example.py
class Car:
	--snip--

	def update_odometer(self, mileage):
		--snip--

	def increment_odometer(self, miles):
		"""Add the given amount to the odometer reading."""
		self.odometer_reading += miles

my_used_car = Car('subaru', 'outback', 2019)
print(my_used_car.get_descriptive_name())

my_used_car.update_odometer(23_500)
my_used_car.read_odometer()

my_used_car.increment_odometer(100)
my_user_car.read_odometer()

"""
2019 Subaru Outback
This car has 23500 miles miles on it.
This car has 23600 miles on it.
"""
```

**Note:** You can use methods like this to control how users of your program update values such as an odometer reading, but anyone with access to the program can set the odometer reading to any value by accessing the attribute directly. Effective security takes extreme attention to detain in addition to basic checks like those shown here.
