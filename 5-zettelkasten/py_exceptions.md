### Meta
2024-11-04 14:33
**Tags:** [[python]] [[py_basics]] [[py_files_exceptions]]
**Status:** #pending 

### Exceptions
Python uses special objects called *exceptions* to manage errors that arise during a program’s execution. Whenever an error occurs that makes Python unsure of what to do next, it creates an exception object. If you write code that handles the exception, the program will continue running. If you don’t, the program will halt and show a *traceback*, which includes a report of the exception that was raised.

Exceptions are handled with `try-except` blocks. A `try-except` block asks Python to do something, but it also tells Python what to do if an exception is raised. When you use `try-except` blocks, your programs will continue running even if things start to go wrong. Instead of tracebacks, which can be confusing for users to read, users will see friendly error messages that you’ve written.

#### Handling the ZeroDivisionError Exception
```Python title:division_calculator.py
print(5/0)

"""
Traceback (most recent call last):
  File "division_calculator.py", line 1, in <module>
    print(5/0)
          ~^~
ZeroDivisionError: division by zero
"""
```

The error reported in the traceback, `ZeroDivisionError`, is an exception object. Python creates this kind of object in response to a situation where it can’t do what we ask it to. When this happens, Python stops the program and tells us the kind of exception that was raised. We can use this information to modify our program.

#### Using try-except Blocks
When you think an error may occur, you can write a `try-except` block to handle the exception that might be raised.
```Python title:example.py
try:
	print(5/0)
except ZeroDivisionError:
	print("You can't divide by zero!")

"""
You can't divide by zero!
"""
```

If more code followed the `try-except` block, the program would continue running because we told Python how to handle the error.

#### Using Exceptions to Prevent Crashes
Handling errors correctly is especially important when the program has more work to do after the error occurs. This happens often in programs that prompt users for input. If the program responds to invalid input appropriately, it can prompt for more valid input instead of crashing.

```Python title:division_calculator.py
print("Give me two numbers, and I'll divide them.")
print("Enter 'q' to quit.")

while True:
	first_number = input("\nFirst number: ")
	if first_number == 'q':
		break
	second_number = input("Second number: ")
	if second_number = 'q':
		break
	answer = int(frist_number) / int(second_number)
	print(answer)
```

This program does nothing to handle errors, so asking it to divide by zero causes it to crash:
```Python title:division_calculator.py
"""
Give me two numbers, and I'll divide them.
Enter 'q' to quit.

First number: 5
Second number: 0
Traceback (most recent call last):
  File "division_calculator.py", line 11, in <module>
    answer = int(first_number) / int(second_number)
             ~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~
ZeroDivisionError: division by zero
"""
```

It’s bad that the program crashed, but it’s also not a good idea to let users see tracebacks. Nontechnical users will be confused by them, and in a malicious setting, attackers will learn more than you want them to. For example, they’ll know the name of your program file, and they’ll see a part of your code that isn’t working properly. A skilled attacker can sometimes use this info to determine which kind of attacks to use against your code.

#### The else Block
We can make this program more error-resistant by wrapping the line that might produce errors in a `try-except` block. The error occurs on the line that performs the division, so that’s were we’ll put the `try-except` block. This example also includes an `else` block. Any code that depends on the `try` block executing successfully goes in the `else` block:
```Python title:division_calculator.py
print("Give me two numbers, and I'll divide them.")
print("Enter 'q' to quit.")

while True:
	first_number = input("\nFirst number: ")
	if first_number == 'q':
		break
	second_number = input("Second number: ")
	if second_number = 'q':
		break
	try:
		answer = int(first_number) / int(second_number)
	except ZeroDivsionError:
		print("You can't divide by 0!")
	else:
		print(answer)

"""
Give me two numbers, and I'll divide them.
Enter 'q' to quit.

First number: 5
Second number: 0
You can't divide by 0!

First number: 5
Second number: 2
2.5

First number: q
"""
```

The only code that should go in a `try` block is code that might cause an exception to be raised. Sometimes you’ll have additional code that should run only if the `try` block was successful; this code goes in the `else` block. The `except` block tells Python what to do in case a certain exception arises when it tries to run the code in the `try` block.

#### Handling the FileNotFoundError Exception
```Python title:alice.py
from pathlib import Path

path = Path('alice.txt')
contents = path.read_text(encoding='utf-8')
```

Note that we’re using `read_text()` in a slightly different way here than what you saw earlier. The `encoding` argument is needed when your system’s default encoding doesn’t match the encoding of the file that’s being read. This is most likely to happen when reading from a file that wasn’t created on your system.

Python can’t read from a missing file, so it raises an exception:
```Python title:example.py
"""
Traceback (most recent call last):
  File "alice.py", line 4, in <module>
    contents = path.read_text(encoding='utf-8')
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
File "path/.../pathlib.py", line 1056, in read_text
  with self.open(mode='r', encoding=encoding, errors=errors) as f:
       ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
File "/.../pathlib.py", line 1042, in open
  return io.open(self, mode, buffering, encoding, errors, newline)
         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

FileNotFoundError: [Errno 2] No such file or directory: 'alice.txt'
"""
```

This is a longer traceback than what we’ve encountered thus far, so let’s make sense of it. It’s best to start at the very end of the traceback.

On line `13`, we can see that a `FileNotFoundError` exception was raised. This tells us what kind of exception to use in the `except` block that we’ll write.

On line `3`, we an see that the error occurred at line `4` in the file *alice.py*. The next line shows the line of code that caused the error. The rest of the traceback shows some code from the libraries that are involved in opening and reading from files. You don’t usually need to read through or understand all of these lines in a traceback.

To handle the error that’s being raised, the `try` block will begin with the line that was identified as problematic in the traceback. In our example, this is the line that contains `read_text()`:
```Python title:alice.py
from pathlib import Path

path = Path('alice.txt')
try:
	contents = path.read_text(encoding='utf-8')
except FileNotFoundError:
	print(f"Sorry, the file {path} does not exist.")
```

In this example, the code in the `try` block produces a `FileNotFoundError`, so we write an `except` block that matches that error. Python then runs the code in that block when the file can’t be found, and the result is a friendly error message instead of a traceback:
```Python title:alice.py
"""
Sorry, the file alice.txt does not exist.
"""
```

The program has nothing more to do if the file doesn’t exist, so this is all the output we see.

#### Analyzing Text
```Python title:alice.py
from pathlib import Path

path = Path('alice.txt')
try:
	contents = path.read_text(encoding='utf-8')
except FileNotFoundError:
	print(f"Sorry, the file {path} does not exist.")
else:
	# Count the approximate number of words in the file:
	words = contents.split()
	num_words = len(words)
	print(f"The file {path} has about {num} words.")

"""
The file text_files/alice.txt has about 29564 words.
"""
```

The method `split()` splits a string wherever it finds a whitespace (by default).

#### Working with Multiple Files
Let’s add more books to analyze. First, we move the bulk of this program to a function called `count_words`. This will make it easier to run the analysis for multiple books:
```Python title:word_count.py
from pathlib import Path

def count_words(path):
	"""Count the approximate number of words in a file. """
	try:
		contents = path,read_text(encoding='utf-8')
	except FileNotFoundError:
		print(f"Sorry, the file {path} does not exist.")
	else:
		# Count the approximate number of words in the file:
		words = contents.split()
		num_words = lent(words)
		print(f"The file {path} has about {num_words} words.")

path = Path('alice.txt')
count_words(path)
```

Now we can write a short loop to count the words in any text we want to analyze. We do this by storing the names of the files we want to analyze in a list, and then we can call `count_words()`  for each file in the list. We’ll try to count the words for *Alice in Wonderland*, *Siddhartha*, *Moby Dick*, and *Little Women*, all part of the public domain. *Siddhartha* is intentionally left out, to test our program.

```Python title:word_count.py
from pathlib import Path

def count_words(path):
	"""Count the approximate number of words in a file. """
	try:
		contents = path,read_text(encoding='utf-8')
	except FileNotFoundError:
		print(f"Sorry, the file {path} does not exist.")
	else:
		# Count the approximate number of words in the file:
		words = contents.split()
		num_words = len(words)
		print(f"The file {path} has about {num_words} words.")

filenames = ['alice.txt', 'siddhartha.txt', 'moby_dick.txt', 'little_women.txt']
for filename in filenames:
	path = Path(filename)
	count_words(path)

"""
The file alice.txt has about 29594 words.
Sorry, the file siddhartha.txt does not exist.
The file moby_dick.txt has about 215864 words.
The file little_women.txt has about 189142 words.
"""
```

Using the `try-escept` block here provides two significant advantages. We prevent our users from seeing a traceback, and we let the program continue analyzing the texts it’s able to find. If we don’t catch the `FileNotFoundError` that *siddhartha.txt* raises, the user would see a full traceback, and the program would stop running after trying to analyze *Siddhartha*.

#### Failing Silently
In the previous example, we informed our users that one of the files was unavailable. But you don’t need to report every exception you catch. Sometimes, you' want the program to fail silently when an exception occurs and continue on as if nothing happened. To achieve that, we explicitly tell Python to do nothing in the `except` block with a `pass` statement.
```Python title:example.py
def count_words(path):
	"""Count the approximate number of words in a file."""
	try:
		--snip--
	except FileNotFoundError:
		pass
	else:
		--snip--

"""
The file alice.txt has about 29594 words.
The file moby_dick.txt has about 215864 words.
The file little_women.txt has about 189142 words.
"""
```

The `pass` statement also acts as a placeholder. It’s a reminder that you’re choosing to do nothing at a specific point in your program’s execution and that you might want to do something there later.

#### Deciding Which Errors to Report
Every time your program depends on something external, such as user input, the existence of a file, or the availability of a network connection, there is a possibility an exception being raised.