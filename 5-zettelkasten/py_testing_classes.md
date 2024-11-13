### Meta
2024-11-11 21:03
**Tags:** [[python]] [[py_basics]] [[py_testing]]
**Status:** #completed 

### Testing a Class
You’ll use classes in many of your own programs, so it’s helpful to be able to prove that your classes work correctly. If you have passing tests for a class you’re working on, you can be confident that improvements you make to the class won’t accidentally break its current behavior.

#### A Variety of Assertions
When writing a test, you can make any claim that can be expressed as a conditional statement. If the condition is `True` as expected, your assumption about how that part of your program behaves will be confirmed; you can be confident that no errors exist.

*Table:* Commonly Used Assertion Statements in Tests

| Assertion                    | Claim                                    |
| ---------------------------- | ---------------------------------------- |
| `assert a == b`              | Assert that two values are equal.        |
| `assert a != b`              | Assert that two values are not equal.    |
| `assert a`                   | Assert that `a` evaluates to `True`.     |
| `assert not a`               | Assert that `a` evaluates to `False`.    |
| `assert element in list`     | Assert that an element is in a list      |
| `assert element not in list` | Assert that an element is not in a list. |

#### A Class to Test
```Python title:survey.py
class AnonymousSurvey:
	"""Collect anonymous answers to a survey question."""

	def __init__(self, question):
		"""Store a question, and prepare to store responses."""
		self.question = question
		self.responses = []

	def show_question(self):
		"""Show the survey question."""
		print(self.question)

	def store_response(self, new_response)
		"""Store a single response to the survey."""
		self.response.append(new_response)

	def show_results(self):
		"""Show all the responses that have been given."""
		print("Survey results:")
		for response in self.responses:
			print(f"- {response}")
```

To show that the `AnonymousSurvey` class works, let’s write a program that uses the class:
```Python title:language_survey.py
from survey import AnonymousSurvey

# Define a question, and make a survey.
question = "What language did you first learn to speak?"
language_survey = AnonymousSurvey(question)

# Show the question, and store responses to the question
language_survery.show_question()
print("Enter 'q' at any time to quit.\n")
while True:
	response = input("Language: ")
	if response == 'q':
		break
	language_survey.store_response(response)

# Show the survey results.
print("\nThank you to everyone who participated in the survey!")
language_survey.show_results()
```

#### Testing the AnonymousSurvey Class
```Python title:test_survey.py
from survey import AnonymousSurvey

def test_store_single_response():
	"""Test that a single response is stored properly."""
	question = "What language did you first learn to speak?"
	language_survey = AnonymousSurvey(question)
	language_survey.store_response('English')
	assert 'English' in language_survey.responses
```

By default, running `pytest` with no arguments will run all the tests that `pytest` discovers in the current directory. To focus on the tests in one file, pass the name of the test file you want to run.

``` BASH title:example.sh
pytest test_survey.py
=================== test session starts ==============
--snip--
test_survey.py .                                [100%]
=================== 1 passed in 0.01s ================
```

This is a good start, but a survey is useful only if it generates more than one response. Let’s verify that three responses can be stored correctly. To do this, we add another method to `TestAnonymousSurvey`:
```Python title:test_survey.py
from survey import AnonymousSurvey

def test_store_single_response():
	--snip--

def test_store_three_responses():
	"""Test that three individual responses are stored properly."""
	question = "What language did you first learn to speak?"
	language_survey = AnonymousSurvey(question)
	responses = ['English', 'Italian', 'Greek']
	for response in responses:
		language_survey.store_response(response)

	for response in responses:
		assert response in language_survey.responses
```

When we write the file again, both tests pass:
```BASH title:example.sh
pytest test_survey.py
=================== test session starts =============
--snip--
test_survey.py ..                              [100%]
================= 2 passed in 0.01s =================
```

These tests work, but are a bit repetitive.

#### Using Fixtures
In testing, a *fixture* helps set up a test environment. Often, this means creating a resource that’s used by more than one test. We create a fixture in `pytest` by writing a function with the decorator `@pytest.fixture`.

A *decorator* is a a directive placed just before a function definition; Python applies this directive to the function before it runs, to alter how the function code behaves.

```Python title:test_survey.py
import pytest
from survey import AnonymousSurvey

@pytest.fixture
def language_survey():
	"""A survey that will be available to all test functions."""
	question = "What language did you first learn to speak?"
	language_survey = AnonymousSurvey(question)
	return language_survey

def test_store_single_response(language_survey):
	"""Test that a single response is stored properly."""
	language_survey.store_response('English')
	assert 'English' in language_survey.responses

def test_store_three_responses(language_survey):
	"""Test that three individual responses are stored properly."""
	responses = ['English', 'Spanish', 'Mandarin']
	for response in responses:
		language_survey.store_response(response)

	for response in responses:
		assert response in language_survey.responses
```