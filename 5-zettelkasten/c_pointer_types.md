### Meta
2024-10-25 22:16
**Tags:** [[c]] [[c_objects_functions_types]] [[c_derived_types]]
**Status:** #completed 

### Pointer Types
A *pointer type* is derived from the function or object type that it points to, called the *referenced* type. A pointer provides a reference to an entity of the referenced type.

The following three declarations declare a pointer to *int*, a pointer to *char*, and a pointer to *void*:
```C title:pointer_types_declarations.c
int *p;
char *cp;
void *vp;
```

Earlier in the chapter, we were introduced to the address-of (`&`) and indirection (`*`) operators. You use the `&` operator to take the address of an object or function. If the object is an `int`, for example, the result of the operator has the type pointer to `int`:
```C title:pointer_to_int.c
int i = 17;
int *ip = &i;
```

We declare the variable `ip` as a pointer to `int` and assign it the address of `i`. You can also use the `&` operator on the result of the `*` operator:
```C title:pointer_to_int.c
ip = &*ip;
```

Dereferencing `ip` by using the indirection operator resolves to the actual object `i`. Taking the address of `*ip` by using the `&` operator retrieves the pointer, so these two operations cancel each other out.

The unary `*` operator converts a pointer to a type into a value of that type. It denotes *indirection* and operates only on pointers. If the operand points to a function, the result of using the `*` operator is the function designator, and if it points to an object, the result is a value of the designated object. For example, if the operand is a pointer to `int`, the result of the indirection operator has the type `int`. If the pointer is not pointing to a valid object or function, bad things may happen.