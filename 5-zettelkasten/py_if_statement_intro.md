### Meta
2024-10-30 12:39
**Tags:** [[python]] [[py_basics]] [[py_conditionals]]
**Status:** #completed 

### A Simple Example
```Python title:example.py
cars = ['audi', 'bmw', 'subaru', 'toyota']

for car in cars:
	if car == 'bmw':
		print(car.upper())
	else:
		print(car.title())

"""
	Output:
Audi
BMW
Subaru
Toyota
"""
```