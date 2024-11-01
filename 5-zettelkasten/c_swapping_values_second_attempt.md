### Meta
2024-10-24 14:14
**Tags:** [[c]] [[c_objects_functions_types]] [[c_declaring_variables]]
**Status:** #pending 

### Swapping Values (Second Attempt)
To repair [[c_swapping_values_first_attempt|this bug]], you can use pointers to rewrite the `swap` function.

We use the *indirection* operator (`*`) to both declare pointers and dereference them, as shown below:

*Listing 2-3: The revised `swap` function using pointers*
```C title:swapper_revised.c
void swap(int *pa, int *pb) {
	int t = *pa;
	*pa = *pb;
	*pb = t;
	return;
}
```

When used in a function declaration or definition, `*` acts as part of a pointer declarator indicating that the parameter is a pointer to an object or function of a specific type.

In the rewritten `swap` function, we specify two parameters `pa` and `pb`, and declare them both as type pointers to `int`.

When using the unary `*` operator in expressions within the function, the unary `*` operator dereferences the pointer to the object. For example:

```C title:example.c
pa = pb;
```

This replaces the value of the pointer `pa` with the value of the pointer `pb`. Now consider the actual assignment in the `swap` function:
```C title:swapper_revised.c
*pa = *pb;
```

This dereferences the pointer `pb`, reads the referenced value, dereferences the pointer `pa`, and then overwrites the value at the location referenced by `pa` with the value referenced by `pb`.

When you call the `swap` function in `main`, you must also place an ampersand (`&`) character before each variable name:
```C title:swapper_revised.c
swap(&a, &b);
```

The unary `&` is the *address-of* operator, which generates a pointer to its operand. This change is necessary because the `swap` function now accepts pointers to objects of type `int` as parameters instead of simply values of type `int`.

*Listing 2-4: Simulated call-by-reference*
```C title:swapper_revisited
#include <stdio.h>
void swap(int *pa, int *pb) // pa -> a: 21    pb -> b: 17
{
	int t = *pa;            // t: 21
	*pa = *pb;              // pa -> a: 17    pb -> b: 17 
	*pb = t;                // pa -> a: 17    pb -> b: 21
}

int main(void)
{
	int a = 21;             // a: 21
	int b = 17;             // b: 17
	swap(&a, &b);
	printf("a = %d, b = %d\n", a, b);    // a: 17    b: 21
	return 0;
}
```

Upon entering the `main` block, the variables `a` and `b` are initialized to `21` and `17`, respectively. The code then takes the addresses of these objects and passes them to the `swap` function as arguments.

Within the `swap` function, the parameters `pa` and `pb` now both declared to have the type pointer to `int` and contain copies of the arguments passed to `swap` from the calling function (here, `main`). These address copies still refer to the exact same objects, so when the values of the objects they reference are swapped in the `swap` function, the contents of the original objects declared in `main` are accessed and also swapped.

This approach simulates *call-by-reference* (aka *pass-by-reference*) by generating object addresses, passing those by value, and then dereferencing the copied address to access the original objects.