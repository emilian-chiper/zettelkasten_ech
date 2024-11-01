### Meta
2024-10-25 12:39
**Tags:** [[c]] [[c_objects_functions_types]]
**Status:** #completed 

### Storage Duration
Objects have storage duration that determines their lifetime.

Four storage durations are available: automatic, static, thread, and allocated.

Objects of automatic storage duration are declared within a block or as a function parameter. The lifetime of these objects begins when the block in which they’re declared begins execution, and ends when execution of the block ends. If the block is entered recursively, a new object is created each time, each with its own storage.

**Note**
	Scope and lifetime are entirely different concepts. *Scope* applies to identifiers, whereas *lifetime* applies to objects. The scope of an identifier is the code region where the object denoted by the identifier can be accessed by its name. The lifetime of an object is the time period for which the object exists.

Objects declared in file scope have *static* storage duration. The lifetime of these objects is the entire execution of the program, and their stored value is initialized prior to program startup. You can also declare a variable within a block scope to have static storage duration using the storage-class specifier `static`, as shown below. These objects persist after the function is exited.

*Lisiting 2-6: A counting example*
```C title:counting.c
voind increment(void) {
	static unsigned int counter = 0;
	counter++;
	printf("%d", counter);
}

int main(void) {
	for (int i = 0; i < 5; i++) {
		increment();
	};
	return 0;
}
```

This program outputs `1 2 3 4 5`. We initialize the static variable `counter` to 0 once at program startup, and increment it each time the `increment` function is called. The lifetime of `counter` is the entire execution of the program, and it will retain its last-stored value throughout its lifetime. You could achieve the same behavior by declaring `counter` with file scope. However, it’s good practice to limit the scope of an object wherever possible.

Static objects must be initialized with a constant value and not a variable:
```C title:static_object.c
int *func(int i) {
	const int j = i; // ok
	static int k = j; // error
	return &k;
}
```

A constant value refers to literal constants (for example, `1`, `a`, or `0xFF`), `enum` members, and the results of operators such as `alignof` or `sizeof`; not `const`-qualified objects.

*Thread* storage duration is used in concurrent programming.

*Allocated* storage duration deals with dynamically allocated memory.