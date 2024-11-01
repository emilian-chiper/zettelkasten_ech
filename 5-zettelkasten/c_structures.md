### Meta
2024-10-25 22:47
**Tags:** [[c]] [[c_objects_functions_types]] [[c_derived_types]]
**Status:** #completed 

### Structures
A *structure type* (aka a `struct`) contains sequentially allocated memory objects. Each object has its own name and may have a distinct type–unlike arrays, which must all be of the same type. Structures are similar to record types found in other programming languages. Listing 2-9 declares an object identified by `sigline` that has a type of `struct sigrecord` and a pointer to the `sigline` object identified by `sigline_p`.

*Listing 2-9: struct sigrecord*
```C title:struct_sigrecord.c
struct sigrecord {
	int signum;
	char signame[20];
	char sigdesc[100];
} sigline, *sigline_p;
```

The structure has three member objects: `signum` is a n object of type `int`, `signame` is an array of type `char` consisting of `20` elements, and `sigdesc` is an array of type `char` consisting of 100 elements.

Structures are useful for declaring collections of related objects and may be used to represent things such as date, customer, or personnel record. They are especially useful for grouping objects that are frequently passed together as arguments to a function, so you don’t need to repeatedly pass individual objects separately.

Once you’ve defined a structure, you’ll likely want to reference its members. You reference members of an object of the structure type by using the structure member operator `.`. If you have a pointer to a structure, you can reference its members with the structure pointer operator `->`.

*Listing 2-10: Referencing structure members*
```C title:referncing_structs.c
sigline.signum = 5;
strcpy(sigline.signame, "SIGINT");
strcpy(sigline.sigdesc, "Interrupt from keyboard");

sigline_p = &signline;

sigline_p->signum = 5;
strcpy(sigline_p->signame, "SIGINT");
strcpy(sigline_p->sigdesc, "Interrupt from keyboard");
```

The first three lines directly access members of the `sigline` object by using the `.` operator. At line 5, we assign a pointer to `sigline_p` to the address of the `sigline` object. In the final three lines, we indirectly access the members of `sigline` by using the `->` operator through the `signline_p` pointer.