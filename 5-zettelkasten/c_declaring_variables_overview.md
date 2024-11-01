### Meta
2024-10-24 13:46
**Tags:** [[c]] [[c_objects_functions_types]] [[c_declaring_variables]]
**Status:** #completed 

### Declaring variables
When you declare a variable, you assign it a type and provide it a name, or *identifier*, by which to reference the variable.

Below are the declarations of two integer objects with initial values. This simple program also declares, but doesn’t define, a `swap` function to swap those values.

*Listing 2-1: Program meant to swap two integers*
```C title:swapper.c
#include <stdio.h>

void swap(int, int); // defined in Listing 2-2

int main(void)
{
	int a = 21;
	int b = 17;

	swap(a, b);
	printf("main: a = %d, b = %d\n", a, b);
	return 0;
}
```

This example program shows a `main` function with a single code block between the `{ }` characters. This kind of code block is known as a *compound statement*.

We defined two variables, `a` and `b`, within the `main` function. We declared the variables as having the type `int` and initialized them to `21` and `17`, respectively.

Each variable must have a declaration.

The `main` function then calls the `swap` function to try to swap the values of the two integers. The `swap` function is declared in this program, but not defined.

#### Declaring multiple variables
You can declare multiple variables in a single declaration, but doing so can be confusing if they are pointers or arrays, or if they are of different types. These are correct:
```C title:example.c
char *src, c;
int x, y[5];
int m[12], n[15][3], o[21];
```

- The first line declares two variables, `src` and `c`, which have different types. `src` has a type of `char *`, and `c` has a type of `char`.
- The second line declares two variables, `x` and `y`, of different types – `int`, and an array of five elements, respectively.
- The third line declares three arrays, `m`, `n`, and `o`, of different dimensions and numbers of elements.

These declarations are easier to understand if separated:
```C title:example.c
char *src;
char c;
int x;
int y[5];
int m[12];
int n[15][3];
int o[21];
```

Readable and understandable code is less likely to have defects.