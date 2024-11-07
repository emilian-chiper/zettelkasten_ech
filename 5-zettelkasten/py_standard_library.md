### Meta
2024-11-03 22:44
**Tags:** [[python]] [[py_basics]] [[py_classes]]
**Status:** #completed 

### The Python Standard Library
The *Python standard library* is a set of modules included with every Python installation. You can use any function or class in the standard library by including a simple `import` statement at the top of your file.

For example, here’s how to generate a random number between 1 and 6:
```BASH title:example.sh
>>> from random import randing
>>> randint(1, 6)
3
```

Another useful function is `choice()`. This takes in a list or tuple and returns a randomly chosen element:
```BASH title:example.sh
>>> from random import choice
>>> players = ['charles', 'martina', 'michael', 'florence', 'eli']
>>> first_up = choice(players)
>>> first_up
'florence'
```

The `random` module shouldn’t be used when building security-related applications, but it works well for many fun and interesting projects.