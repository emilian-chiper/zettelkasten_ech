### Meta
2024-10-25 22:41
**Tags:** [[c]] [[c_objects_functions_types]] [[c_derived_types]]
**Status:** #completed 

### Type Definitions
You use a `typedef` to declare an alias for an existing type; it never creates a new type. For example, each of the following declarations creates a new type alias:
```C title:type_definitions.c
typedef unsigned int uint_type;
typedef signed char schar_type, *schar_p, (*fp)(void);
```

On the first line, we declare `uint_type` as an alias for the type `unsigned int`. On the second line, we declare `schar_type` as an alias for `signed char`, `schar_p` as an alias for `signed char *`, and `fp` as an alias for `signed char(*)(void)`.

Identifiers that end in `_t` in the standard headers are type definitions (aliases for existing types).

Generally speaking, you should not follow this convention in your own code base because the C Standard reserve identifiers that match the patterns `int[0-0a-z_]*_t` and `uint[0-9a-z_]*_t`, and the Portable Operating System Interface (POSIX) reserves all identifiers that end in `_t`. 

If you define identifiers that use these names, they may collide with names used by the implementation, which can cause problems that are difficult to debug.