### Meta
2024-10-25 12:02
**Tags:** [[c]] [[c_objects_functions_types]]
**Status:** #completed 

### Scope
Objects, functions, macros, and other C language identifiers have *scope* that delimits the contiguous region where they can be accessed. C has four types of scope: file, block, function prototype, and function.

The scope of an object or function identifier is determined by where it is declared. If the declaration is outside any block or parameter list, the identifier has *file scope*, meaning the scope is the entire text file in which it appears as well as any files included after that point.

If the declaration appears inside a block or within the list of parameters, it has *block scope*, meaning that the identifier it declares is accessible only within the block. The identifiers from `a` and `b` from [[c_swapping_values_second_attempt|Listing 2-4]] have block scope and can be used to refer to only these variables within the code block in the `main` function in which they’re defined.

If the declaration appears within the list of parameter declarations in a function prototype (not part of a function definition), the identifier has *function prototype scope*, which terminates at the end of the function declarator.

*Function scope* is the area between the opening `{` of a function definition and its closing `}`. A label name is the only kind of identifier that has function scope. *Labels* are identifiers followed by a colon and identify a statement in a function to which control can be transferred.

Scope can be *nested*, with *inner* and *outer* scopes. e.g., you can have a block scope inside another block scope, and every block scope is defined within a file scope. The inner scope has access to the outer scope, but not vice-versa. As the name implies, any inner scope must be completely contained within the outer scope that encompasses it.

If you declare the same identifier in both the inner scope and the outer scope, the identifier declared in the outer scope is *hidden* by the identifier within the inner scope, which takes precedence. In this case, naming the identifier will refer to the object in the inner scope; the object from the outer scope is hidden and cannot be referenced by its name.

*Listing 2-5: Scope*
```C title:scopes.c
int j; // file scope of j begins

void f(int i) {                   // block scope of i begins
	int j = 1;                    // block scope of j begins; hides file-scope j
	i++;                          // i refers to the function parameter;
	for (int i = 0; i < 2; i++) { // block scope of loop-local i begins
		int j = 2;                // block scope of the inner j begins
		printf("%d\n", j);        // inner j is in scope, prints 2
	}                             // block scope of the inner i and j ends
	printf("%d\n", j);            // the outer j is in scope, prints 1
}                                 // the block scope of i and j ends
```

There’s nothing wrong with this code, provided the comments accurately describe your intent.

Best practice is to use different names for different identifiers to avoid confusion, which leads to bugs.

Using short names such as `i` and `j` is fine for identifiers with small scopes.

Identifiers in large scopes should have longer, descriptive names that are unlikely to be hidden in nested scopes. Some compilers will warn about hidden file identifiers.