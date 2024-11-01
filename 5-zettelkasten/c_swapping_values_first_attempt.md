### Meta
2024-10-24 13:58
**Tags:** [[c]] [[c_objects_functions_types]] [[c_declaring_variables]]
**Status:** #pending 

### Swapping Values (First Attempt)
Each object has a storage duration that determines its *lifetime*, which is the time during program execution for which the object exists, has storage, has a constant address, and retains its last-stored value.

Objects must not be referenced outside their lifetime.

Local variables such as `a` and `b` from [[c_declaring_variables_overview|Listing 2-1]] have *automatic storage duration*, meaning that they exist until execution leaves the block in which they’re defined.

*Listing 2-2: The `swap` function*
```C title:swapper.c
void swap(int a, int b)
{
	int t = a;
	a = b;
	b = t;
	printf("swap: a = %d, b = %d\n", a, b)
}
```

The `swap` function declares two parameters, `a` and `b`, that are passed as arguments to this function.

C distinguishes between `parameters`, which are objects declared as part of the function declaration that acquire a value on entry to the function, and `arguments`, which are comma-separated expressions you include in the function call expression.

We also declare a temporary variable `t` of type `int` and initialize it to the value of `a`. This variable is used temporarily to save the value stored in `a` so that it’s not lost during the swap.

You can now compile and test the complete program by running the generated executable:
```BASH title:script.sh
./a.out
swap: a = 17, b = 21
main: a = 21, b = 17
```

The variables `a` and `b` were initialized to `21` and `17`, respectively. The first call to `printf` within the `swap` function shows these two values swapped, but the second call to `printf` in `main` shows the original values unchanged.

C is a *call-by-value* (aka `pass-by-value`) language. When you provide an argument to a function, the value of that argument is copied into a distinct variable for use within the function.

The `swap` function assigns the values of the objects you pass as arguments to the respective parameters. When the values of the parameters in the function are changed, the values in the caller are unaffected because they are distinct objects. Consequentially, the variables `a` and `b` retain their original values in `main` during the second call to `printf`.

The goal of the program was to swap the values of these two objects. By testing the program, we conclude it has a *bug*.