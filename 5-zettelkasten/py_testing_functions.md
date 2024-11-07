### Meta
2024-11-06 22:21
**Tags:** [[python]] [[py_basics]] [[py_testing]]
**Status:** #pending 

### Testing a Function
Let’s start with a simple function that takes in a first and last name, and returns a neatly formatted full name:
```Python title:name_function.py
def get_formatted_name(first, last):
	"""Generate a neatly formatted full name."""
	full_name = f"{first} {last}"
	return full_name.title()
```

To check if the function works, we’ll make a program that uses this function. The program *names.py* lets users enter a first and last name, and see a neatly formatted full name:
```Python title:names.py
from name_function import get_formatted_name

print("Enter 'q' at any time to quit.")
while True:
	first = input("\nPlease give me a first name: ")
	if first == 'q':
		break
	last = input("Please give me a last name: ")
	if last == 'q':
		break

	formatted_name = get_formatted_name(first, last)
	print(f"\tNeatly formatted name: {formatted_name}.")

"""
Enter 'q' at any time to quit.

Please give me a first name: janis
Please give me a last name: joplin
	Neatly formatted name: Janis Joplin.

Please give me a first name: bob
Please give me a last name: dylan
	Neatly formatted name: Bob Dylan.

Please give me a first name: q
"""
```

#### Unit Tests and Test Cases
A *unit test* verifies that one specific aspect of a function’s behavior is correct. A *test case* is a collection of unit tests that together prove that a function behaves as it’s supposed to, within the full range of situations you expect it to handle.

A good test case considers all possible kinds of input a function could receive and includes tests to represent each of the situations. A test case with *full coverage* includes a full range of unit tests covering all the possible ways you can use a function. Achieving full coverage on a large project can be daunting. It’s often good enough to write tests for your code’s critical behaviors and then aim for full coverage only if the project starts to see widespread use.

#### A Passing Test
The test function will call the function we’re testing, and we’ll make an assertion about the value that’s returned. If our assertion is correct, the test will pass; otherwise, it will fail.
```Python title:test_name_function.py
from name_function import get_formatted_name

def test_first_last_name():
	"""Do names like 'Janis Joplin' work?"""
	formatted_name = get_formatted_name('janis', 'joplin')
	assert formatted_name == 'Janis Joplin'
```

The name of a test file must start with *test_*. When we ask `pytest` to run the tests we’ve written, it will look for any file that begins with *test_*, and run all of the tests inside that file.