### Meta
2024-10-28 17:52
**Tags:** [[python]] [[py_basics]] [[py_variables_simple_data_types]]
**Status:** #completed 

### Identifiers, Objects, and the Assignment Statement
The most important of all Python commands is an *assignment statement*, such as
```Python title:example.py
temparature = 98.6
```

This command establishes temperature as an *identifier* (aka a *name*), and then associates it with the *object* expressed on the right-hand side of the equal sign.

#### Identifiers
Identifiers in Python are *case-sensitive*. They can be composed of almost any combination of letters, numerals, and underscore characters. The primary restrictions are that an identifier cannot begin with a numeral, and that there are 33 reserved keywords that cannot be used.

**Reserved Words**: False, as, continue, else, from, in, not, return, yield, None, assert, def, except, global, is, or, try, True, break, del, finally, if, lambda, pass, while, and, class, elif, for, import, nonlocal, raise, with

The semantics of a Python identifier is most similar to a reference variable in Java or a pointer variable in C++.

Each identifier is implicitly associated with the *memory address* of the object to which it refers. A Python identifier may be assigned to a special object named `None`, serving a similar purpose to a null reference in Java or C++.

Python is *dynamically typed* language, as there is no advance declaration associating an identifier with a particular data type. An identifier can be associated with any type of object, and it can later be reassigned to another object of the same (or different) type.

Although an identifier has no declared type, the object to which it refers to has a definite type.

We can establish an *alias* by assigning a second identifier to an existing object. Continuing the previous example, `original = temperature`.

Once an alias has been established, either name can be used to access the underlying object. If that object supports behaviors that affect its state, changes enacted through an alias will be apparent when using the other alias (because they refer to the same object).

If one of the *names* is reassigned to a new value using a subsequent assignment statement, that does not affect the aliased object, rather it breaks the alias, e.g. `temparature = temperature + 5.0`.

The execution begins with the evaluation of the expression on the right-hand side of the `=` operator. That expression is evaluated based on the *existing* binding of the name temperature, and so the result has value `103.6`.

That result is stored as a new floating-point instance, and only then is the name on the left-hand side of the assignment statement, `temperature`, (re)assigned to the result.