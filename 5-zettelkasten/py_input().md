### Meta
2024-10-31 17:33
**Tags:** [[python]] [[py_basics]] [[py_user_input_while_loops]]
**Status:** #completed 

### How the input() Function Works
The `input()` function pauses your program and waits for the user to enter some text. Once Python receives the user’s input, it assigns that input to a variable to make it convenient for you to work with.

```Python title:example.py
message = input("Tell me something, and I will repeat it back to you: ")
print(message)

"""
Tell me something, and I will repeat it back to you: Hello everyone!
Hello everyone!
"""
```

The `input()` function takes one argument: the *prompt* that we want to display to the user, so they know what kind of info to enter. The program waits while the user enters their response, and continues after the user presses `ENTER`.

#### Writing Clear Prompts
Include a clear, easy-to-follow prompt that tells the user exactly what kind of information you’re looking for.
```Python title:example.py
name = input("Please enter your name: ")
print(f"\nHello, {name}!")
```

Add a space at the end of your prompts (after the colon) to separate the prompt from the user’s response and to make it clear to the user where to enter their text.

Sometimes, multi-line prompts are needed:
```Python title:example.py
prompt = "If you share your name, we can personalize the message you see."
prompt += "\nWhat is your first name? "

name = input(prompt)
print(f"\nHello, {name}!")

"""
If you share your name, we can personalize the message you see.
What is your first name? Eric

Hello, Eric!
"""
```

#### Using int() to Accept Numerical Input
```Python title:example.py
age = input("How old are you? ")
print(age)

"""
'21'
"""
```

This can produce errors within comparison operations:
```Python title:example.py
age = input("How old are you? ")
print(age >= 18)

"""
How old are you? 21
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: '>=' not supported between instances of 'str' and 'int'
"""
```

To address this, we can use type conversion:
```Python title:example.py
age = input("How old are you? ")
age = int(age)
print(age >= 18)

"""
How old are you? 21
True
"""
```

Another example:
```Python title:example.py
height = input("How tall are you, in inches? ")
height = int(height)

if height >= 48:
	print("\nYou're tall enough to ride!")
else:
	print("\nYou'll be able to ride when you're a little older.")

"""
How tall are you, in inches? 71

You're tall enough to ride!
"""
```

#### The Modulo Operator
```BASH title:example.sh
>>> 4 % 3
1
>>> 5 % 3
2
>>> 6 % 3
0
>>> 7 % 3
1
```

Modulo tells you the remainder of a division operator. When a number is divisible by another, the remainder is `0`, so the modulo operator `%` returns `0`.
```Python title:example.py
number = input("Enter a number, and I'll tell you if it's even or odd: ")
number = int(number)

if number % 2 == 0:
	print(f"\nThe number {number} is even.")
else:
	print(f"\nThe number {number} is odd.")

"""
Enter a number, and I'll tell you if it's even or odd: 42

The number 42 is even
"""
```