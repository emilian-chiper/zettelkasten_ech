### Meta
2024-10-31 18:19
**Tags:** [[python]] [[py_basics]] [[py_user_input_while_loops]]
**Status:** #pending 

### The while Loop in Action
```Python title:example.py
current_number = 1
while current_number <= 5:
	print(current_number)
	current_number += 1

"""
1
2
3
4
5
"""
```

### Letting the user Choose When to Quit
```Python title:example.py
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program."

message = ""
while message != 'quit':
	message = input(prompt)
	print(message)

"""
Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. Hello everyone!
Hello everyone!

Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. Hello again.
Hello again.

Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. quit
quit
"""
```

A small fix:
```Python title:example.py
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program."

message = ""
while message != 'quit':
	message = input(prompt)

	if message != 'quit':
		print(message)

"""
Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. Hello everyone!
Hello everyone!

Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. Hello again.
Hello again.

Tell me something, and I will repeat it back to you:
Enter 'quit' to end the program. quit
"""
```

### Using a Flag
For a program that should run only as long as many conditions are true, you can define one variable that determines whether or not the entire program is active. This variable, called a *flag*, acts as a signal to the program. We can write our programs so they run while the flag is set `True` and stop running when any of several events sets the value of the flag to `False`. As a result, our overall `while` statement needs to check only one condition: whether the flag is currently `True`. Then, all our other tests can be neatly organized in the rest of the program.

```Python title:example.py
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program."

active = True
while active:
	message = input(prompt)

	if message == 'quit':
		active = False
	else:
		print(message)
```

### Using break to Exit a Loop
To exit a `while` loop immediately without running any remaining code in the loop, regardless of the results of any conditional test, use the `break` **statement**.

```Python title:example.py
prompt = "\nPlease enter the name of a city you have visited:"
prompt += "\b(Enter 'quit' when you are finished.) "

while True:
	city = input(prompt)

	if city == 'quit':
		break
	else:
		print(f"I'd love to go to {city.title()}!")

"""
Please enter the name of a city you have visited:
(Enter 'quit' when you are finished.) New York
I'd love to go to New York!

Please enter the name of a city you have visited:
(Enter 'quit' when you are finished.) San Francisco

Please enter the name of a city you have visited:
(Enter 'quit' when you are finished.) quit
"""
```

**Note:** You can use the `break` statement in any of Python’s loops. For example, you could use `break` to quit a `for` loop that’s working through a list or a dictionary.

### Using continue in a Loop
```Python title:example.py
current_number = 0
while current_number < 10:
	current_number += 1
	if current_number % 2 == 0:
		continue

	print(current_number)

"""
1
3
5
7
9
"""
```

### Using continue in a Loop
```Python title:example.py
current_number = 0
while current_number < 10:
	current_number += 1
	if current_number % 2 == 0:
		continue

	print(current_number)

"""
1
3
5
7
9
"""
```

### Avoiding Infinite Loops
```Python title:example.py
x = 1
while x <= 5:
	print(x)
```

Cancel with `<C-c>`.

#### Avoiding Infinite Loops
Test every `while` loop and make sure it stops when you expect it to.
If you want your program to end when the user enters a certain input value, run the program and enter that value.
If the program doesn’t end, scrutinize the way your program handles the value that should cause the loop exit.
Ensure at least one part of the program can make the loop’s condition `False` or cause it to reach  `break` statement.