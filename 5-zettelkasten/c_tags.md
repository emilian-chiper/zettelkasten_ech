### Meta
2024-10-27 21:04
**Tags:** [[c]] [[c_objects_functions_types]]
**Status:** #completed 

### Tags
*Tags* are a special naming mechanism for structs, unions and enumerations. For example, the identifier `s` appearing in the following structure is a tag:
```C title:tag.c
struct s {
	//---snip---
}
```

A tag is not a type name and cannot be used to declare a variable. Instead, you must declare variables of this type as follows:
```C title:declarations.c
struct s v; // instance of struct s
struct s *p; // pointer to struct s
```

The names of unions and enumerations are also tags and not types.

```C declarations.c
enum day { sun, mon, tue, wed, thu, fri, sat };
day today; // error
enum day tomorrow; // OK
```

The tags of structures, unions and enumerations are defined in a separate *namespace* from ordinary identifiers. This allows a C program to have both a tag and another identifier with the same spelling in the same scope:

```C title:declarations.c
enum status { ok, fail }; // enumeration
enum status status(void); // function
```

You can even declare an object `s` of type `struct s`:
```C title:declarations.c
struct s s;
```

It is a bad practice. You can think of `struct` tags as type names and define an alias for the tag by using a `typedef`. Here’s an example:

```C title:alias.c
typedef struct s { int x; } t;
```

This now allows you to declare variables of type `t` instead of `struct s`. The tag name in `struct`, `union`, and `enum` is optional, so you can just dispense with it entirely:

```C title:dispense.c
typedef struct { int x; } t;
```

This works fine except in the case of self-referential structures that contain pointers to themselves:

```C title:self-referential_structs.c
struct tnode {
	int count;
	struct tnode *left;
	struct tnode *right;
};
```

If you omit the tag on the first line, the compiler may complain because the referenced structure on lines 3 and 4 has not yet been declared, or because the whole structure is not used anywhere. Consequentially, you have no choice but to declare a tag for the structure, but you can declare a `typedef` as well:

```C title:typedef.c
typedef struct tnode {
	int count;
	struct tnode *left;
	struct tnode *right;
}
```

Most C programmers use a different name for the tag and the `typedef`, but the same name works just fine. You can also define this type before that structure so that you can use it to declare the `left` and `right` members that refer to other objects of type `tnode`:

```C title:example.c
typedef struct tnode tnode;
struct tnode {
	int count;
	tnode *left;
	tnode *right;
} tnode;
```

Type definitions can improve code readability beyond their use with structures. For example, all three of the following declarations of the `signal` function specify the same type:

```C title:typedef.c
typedef void fv(int), (*pfv)(int);

void (*signal(int, void (*)))(int);
fv *signal(int, fv *);
pfv signal(int, pfv);
```