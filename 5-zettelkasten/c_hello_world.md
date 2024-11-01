### Meta
2024-10-24 11:05
**Tags:** [[c]] [[c_getting_started]]
**Status:** #completed 

### Prerequisites
- A text editor, or
- An Integrated Development Environment (IDE)

### Hello, world! in C
```C title:hello.c
#include <stdio.h>
#include <stdlib.h>
int main(void) {
	puts("Hello, world!");
	return EXIT_SUCCESS;
}
```

#### Compiling and Running Your Program
On Linux and other Unix-like operating systems, you can invoke the system compiler with the `cc` command.

```BASH title:script.sh
cc hello.c
```

If the program was written correctly, the compile command will create a new file called `a.out` in the same directory as your source code.

The `a.out` file is the executable program, which you can now run with:"

```BASH title:script.sh
./a.out
Hello, world!
```

The `cc` command has numerous flags and compiler options. The `-o` file flag lets you give the executable  a file name instead of `a.out`.

```BASH title:script.sh
cc -o hello hello.c
./hello
Hello, world!
```

#### Preprocessor Directives
The first two lines of the `hello.c` program use the `#include` preprocessor directive, which behaves as if you replaced it with the contents of the specified file at the exact same location.

We include the `<stdio.h>` and `<stdlib.h>` headers to access the functions declared in those headers, which we can then call from the program.

The `puts` function is declared in `<stdio.h>`, and the `<EXIT_SUCCESS>` is defined in `<stdlib.h>`.

As the name suggests, `<stdio.h>` contains the declarations for C Standard I/O functions, and `<stdlib.h>` contains the declarations for general utility functions.

You must include the declarations for any library functions that you use in your program.

#### The main Function
The main portion of the program starts with

```C title:hello.c
int main(void) {
```

This line defines the `main` function that’s called at program startup. It defines the main entry point for program execution in a hosted environment when the program is invoked from the command line or another program.

C defines two possible execution environments: *freestanding* and *hosted*.

A freestanding environment may not provide an operating system and is typically used in embedded programming.

We define `main` to return a value of type `int` and place `void` inside the parenthesis to indicate that the function does not accept arguments.

The `int` type is a signed integer type that can be used to represent both positive and negative integer values as well as zero.

Similar to other procedural languages, C programs consist of procedures (referred to as *functions*) that can accept arguments and return values.

Each function is a reusable unit of work that you can invoke as frequently as necessary in your program.

In the example above, the return value of the `main` function indicates whether the program terminated successfully. The actual work performed by this particular function is to print out the line `Hello, world!`.

```C title:hello.c
	puts("Hello, world!");
```

The `puts` function is a C Standard Library function that writes a string argument to `stdout`, which typically represents the console or terminal window, and appends a newline character to the output.

`Hello, world!` is a string literal that behaves like a read-only string.

This function invocation outputs `Hello, world!` to the terminal.

Once your program has completed, you want it to exit. You can do that using the `return` statement within the `main` function to return an integer value to the host environment or invoking script:

```C title:hello.c
	return EXIT_SUCCESS;
```

`EXIT_SUCCESS` is an object-like macro that commonly expands to 0 and is typically defined as follows:

```C title:example.c
#define EXIT_SUCCESS 0
```

Each occurrence of `EXIT_SUCCESS` is replaced by a 0, which is then returned to the host environment from the call to `main`. The script that invokes the function can then check its status to determine whether the invocation was successful. A return from the initial call to the `main` function is equivalent to calling the C Standard Library `exit` function with the value returned by the `main` function as its arguments.

The final line of this program consists of a closing brace `}`, which encloses the code block we started with the declaration of the main function:

```C title:hello.c
int main(void) {
	// ---snip---
}
```

You can place the opening brace on the same line as the declaration or its own line:

```C title:example.c
int main(void)
{
	// ---snip---
}
```

This is a stylistic decision. Be consistent.

#### Checking Function Return Values
Functions often return a value that’s the result of a computation that signifies whether the function successfully completed its task. For example, the `puts` function in our example takes a string to print and returns a value of type `int`. The `puts` function returns the value of the macro `EOF` (a negative integer) if a write error occurs; otherwise, it returns a non-negative integer value.

Although it’s unlikely that the `puts` function will fail and return `EOF` for our simple program, it’s possible. Because the call to `puts` can fail and return `EOF`, it means that your first C program has a bug or, at least, can be improved, as follows:

```C title:hello_improved.c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
	if (puts("Hello, world!") === EOF) {
		return EXIT_FAILURE;
		// code here never executes
	}
	return EXIT_SUCCESS;
	// code here never executes
}
```

This revisited version checks if the `puts` call returns the value `EOF`, indicating a write error.

If the function returns `EOF`, the program returns the value of the `EXIT_FAILURE` macro (which evaluates to a nonzero value). Otherwise, the function succeeds, and the program returns `EXIT_SUCCESS` (which is required to be `0`). The script that invokes the program can then check its status to determine whether it was successful.

Code following a return statement is *dead code*. It never executes.

#### Formatted Output
The to print formatted output, use `printf` over `puts`.

The `printf` function takes a format string that defines how the output is formatted, followed by a variable number of arguments that are the actual values you want to print.

```C title:printf.c
printf("%s\n", "Hello, world!");
```

The first argument is the format string `"%s\n"`. The `%s` is a conversion specification that instructs `printf` to read the second argument (a string literal) and print it to `stdout`. The `\n` is an alphabetic escape sequence used to represent nongraphic characters, and tells `printf` to include a new line after the string. Without the newline sequence, the next characters printed (likely the command prompt) would appear on the same line.

⚠️ Take care not to pass user-supplied data as part of the first argument to the `printf` function, because doing so can result in a formatted output security vulnerability.

If you use the `printf` instead of `puts` in the revised version of the program, it will no longer work, because `printf` returns status differently than `puts`.