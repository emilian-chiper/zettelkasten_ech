### Meta
2024-11-03 23:23
**Tags:** [[python]] [[py_basics]] [[py_files_exceptions]]
**Status:** #completed 

### Reading from a File
When you want to work with the information in a text file, the first step is to read the file into memory. You can then work through all of the file’s contents at once or work through the contents line by line.

#### Reading the Contents of a File
Let’s start with a file that contains $pi$ ti 30 decimal places, with 10 decimal places per line:
```TXT title:pi_digits.txt
3.1415926535
  8979323846
  2643383279
```

Here’s a program that opens this file, reads it, and prints the contents of the file to the screen:
```Python title:file_reader.py
from pathlib import Path

path = Path('pi_digits.txt')
contents = path.read_text()
print(contents)

"""
3.1415926535
  8979323846
  2643383279
  
"""
```

A *path* is the exact location of a file or folder on a system. Python provides a module called `pathlib` that makes it easier to work with files and directories, no matter which operating system you or your program’s users are working with. A module that provides specific functionality like this is often called a *library*.

The only difference between the output and the original file is the extra blank line at the end of the output. The blank line appears because `read_texT()` returns an empty string when it reaches the end of the file; this empty string shows up as a blank line. We can remove it with `rstrip()`:
```Python title:file_reader.py
from pathlib import Path

path = Path('pi-digits.txt')
contents = path.read_text()
contents = contents.rstrip()
# Alternative: contents = path.read_text().rstrip()
print(contents)

"""
3.1415926535
  8979323846
  2643383279
"""
```

On line `6` we see what’s know as *method chaining*.

#### Relative and Absolute File Paths
When you pass *pi_digits.txt* to `Path`, Python looks in the directory where the file that’s currently being executed (i.e. *file_reader.py*) is stored. Sometimes, files might be stored in different directories.

There are two main ways to specify paths in programming.

A *relative path* tells Python to look for a given location relative to the directory where the currently running program file is stored.
```Python title:file_reader.py
path = Path('text_files/filename.txt')
```

You can also tell Python exactly where the file is on your computer, regardless of where the program that’s being executed is stored. This is called an *absolute file path*.

Absolute paths are usually longer than relative paths, because they start at your system’s root folder:
```Python title:example.py
path = Path('/home/emiliano_/data_files/text_files/filename.txt)
```

#### Accessing a File’s Lines
You can use the `splitlines()` method to turn a long string into a set of lines, and then use a `for` loop to examine each line from a file, one at a time.
```Python title:file_reader.py
from pathlib import Path

path = Path('pi_digits.txt')
contents = path.read_text()

lines = contents.splitlines()
for line in lines:
	print(line)

"""
3.1415926535
 8979323846
 2643383279
"""
```

#### Working with a File’s Contents
```Python title:pi_string.py
from pathlib import Path

path = Path('pi_digits.txt')
contents = path.read_text()

lines = contents.splitlines()
pi_string = ''
for line in lines:
	pi_string += line.lstrip()

print(pi_string)
print(len(pi_string))

"""
3.141592653589793238462643383279
32
"""
```

**Note:** When Python reads from a text file, it interprets all text in the file as a string. If you read in a number and want to work with that value in a numerical context, you’ll have to convert it to an integer using the `int()` function or a float using the *float()* function.

#### Large Files: One Million Digits
If we start with a text file that contains $pi$ up to 1,000,000 decimal places, instead of just 30, we can create a single string containing all these digits. We don’t need to change our program at all, except to pass it a different file. We’ll also print just the first 50 decimal places, so we don’t have to watch a million digits scroll by in the terminal:
```Python title:pi_string.py
from pathlib import Path

path = Path('pi_million_digits.txt')
contents = path.read_text()

lines = contents.splitlines()
pi_string = ''
for line in lines:
	pi_string += line.lstrip()

print(f"{pi_string[:52]}...")
print(len(pi_string))

"""
3.14159265358979323846264338327950288419716939937510...
1000002
"""
```

#### Is Your Birthday Contained in Pi?
Let’s use the program we just wrote to find out if someone’s birthday appears anywhere in the first million digits of $pi$. We can do this by expressing each birthday as a string of digits and seeing if that string appears anywhere in `pi_string`:
```Python title:pi_birthday.py
from pathlib import Path

path = Path('pi_million_digits.txt')
contents = path.read_text()

lines = contents.splitlines()
pi_string = ''
for line in lines:
	pi_string += line.lstrip()

birthday = input("Enter your birthday, in the form mmddyy: ")
if birthday in pi_string:
	print("Your birthday appears in the first million digits of pi!")
else:
	print("Your birthday does not appear in the first million digits digits of pi.")

"""
Enter your birthdate, in the form mmddyy: 120372
Your birthday appears in the first million digits of pi!
"""
```