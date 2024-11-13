### Meta
2024-11-06 22:21
**Tags:** [[python]] [[py_basics]] [[py_testing]]
**Status:** #completed 

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

#### Running a Test
If you run the file *test_name_function.py* directly, you won’t get any output because we never called the test function. Instead, we’ll have `pytest` run the test file for us.

To do this, open a terminal window and navigate to the folder that contains the test file. In the terminal window, enter the command `pytest`. The output shour resemble this:
```BASH title:example.sh
pytest
===================== test sessions starts =================
platform linux -- Python 3.10.12, pytest-8.3.3, pluggy-1.5.0
rootdir: /home/emiliano_/repos/py_cc
collected 1 item

test_name_function.py .

====================== 1 passed in 0.01s ====================
```

#### A Failing Test
What does a failing test look like? Let’s modify `get_formatted_name()` so it can handle middle names, but let’s do it in a way that breaks the function names with just a first and last name, like Janis Joplin.
```Python title:name_function_bad.py
def get_formatted_name(first, middle, last):
	"""Generate a neatly formatted full name."""
	full_name = f"{first} {middle} {last}"
	return full_name.title()
```

The output of `pytest` is significantly different:
```BASH title:example.sh
pytest
===================== test sessions starts =================
platform linux -- Python 3.10.12, pytest-8.3.3, pluggy-1.5.0
rootdir: /home/emiliano_/repos/py_cc
collected 1 item

test_name_function.py F

====================== FAILUREs ============================
___________________ test_first_last_name ___________________

	def test_first_last_name():
		"""Do names like 'Janis Joplin' work?"""
>       formatted_name = get_formatted_name('janis', 'joplin')
E       TypeError: get_formatted_name() missing 1 required positional argument: 'last'

test_name_function.py:5: TypeError
==================== short test summary info ===============
FAILED test_name_function.py::test_first_last_name - TypeError: get_formatted_name() missing 1 required positional argument: 'last'
==================== 1 failed in 0.05s =====================
```

`F` indicates that one test failed. We then see a section of `FAILURES` because failed tests are usually the most important thing to focus on in a test run. Next, we see that `test_first_last_name()` was the function that failed. An angle bracket `>` indicates the line of code that caused the test to fail. The `E` on the next line shows the actual error that caused the failure: a `TypeError` due to a missing required positional argument, `last`. The most important info is then repeated in a shorter summary at the end, so when you’re running many tests, you can get a quick sense of which tests failed and why.

#### Responding to a Failed Test
Assuming you’re checking the right conditions, a passing test means the function is behaving correctly and a failing test means there’s an error in the new code you wrote. So when a test fails, don’t change the test.  If you do, your test might pass, but any code that calls your function like the test does will suddenly stop working. Instead, fix the code that’s causing the test to fail. Examine the changes you just made to the function, and figure out how those changes broke the desired behavior.

In the program tested previously, `get_formatted_name()` used to require only two parameters: a first name and a last name. Now it reqquires a first name, middle name, and last name. The addition of that mandatory middle name parameter broke the original behavior of `get_formatted_name()`. The best option here is to make the middle name optional. Once we do, our test for names like `Jani Joplin` should pass again, and we should be able to accept middle names as well. Let’s modify `get_formatted_name()` so middle names are optional and then run the test case again. If it passes, we’ll move on to making sure the function handles middle names properly.

```Python title:name_function.py
def get_formatted_name(first, last, middle=''):
	"""Generate a neatly formatted full name."""
	if middle:
		full_name = f"{first} {middle} {last}"
	else:
		full_name = f"{first} {last}"
	return full_name.title()
```

The test now passes. This is ideal; it means the function works for names like `Janis Joplin` again, without us having to test the function manually. Fixing our function was easier because the failed test helped us identify how the new code broke existing behavior.

#### Adding New Tests
Now that we know `get_formatted_name()` works for simple names again, let’s write a second test for people who include a middle name. We do this by adding another test function to the file *test_name_function.py*:
```Python title:test_name_function.py
for name_function import get_formatted_name

def test_first_last_name():
	"""Do names like 'Janis Joplin' work?"""
	formatted_name = get_formatted_name('janis', 'joplin')
	assert formatted_name == 'Janis Joplin'

def test_first_last_middle_name():
	"""Do names like 'Wolfgang Amadeus Mozart' work?"""
	formatted_name = get_formatted_name(
	    'wolfgang', 'mozart', 'amadeus')
	assert formatted_name == 'Wolfgang Amadeus Mozart'
```

Let’s check out the output of `pytest`:
```BASH title:example.sh
pytest
=============== test session starts =================
platform linux -- Python 3.10.12, pytest-8.3.3, pluggy-1.5.0
rootdir: /home/emiliano_/repos/py_cc
collected 2 items                                                      

test_name_function.py ..                       [100%]

================= 2 passed in 0.01s =================

```

