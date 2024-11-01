### Meta
2024-10-26 19:39
**Tags:** [[c]] [[c_objects_functions_types]] [[c_derived_types]]
**Status:** #completed 

### Unions
*Unions types* are similar to structures, except that the memory used by the member objects overlaps. Unions can contain an object of one type at one time, and an object of a different type at a different time, but never both objects at the same time, and are primarily used to save memory.

Listing 2-11 shows the union `u` that contains three structures: `n`, `ni`, and `nf`. This union might be used in a tree, graph, or other data structure that has some nodes that contain integer values (`ni`) and other nodes that contain floating-point values (`nf`).

*Listing 2-11: Unions*
```C title:unions.c
union {
	struct {
		int type;
	} n;
	struct {
		int type;
		int intnode;
	} ni;
	struct {
		int type;
		double doublenode;
	} nf;
} u;
u.nf.type = 1;
u.nf.doublenode = 3.14;
```

As with structures, you can access union members via the `.` operator. Using a pointer to a union, you can reference its members with the `->` operator. In Listing 2-11, the `type`  member in the `nf` struct of the union is referenced as `u.nf.type`, and the `doublenode` member is referenced as `u.nf.doublenode`. Code that uses this union will typically check the type of the node by examining the value stored in `u.n.type` and then accessing either the `intnode` or `doublenode` `struct` depending on the type. If this had been implemented as a structure, each node would contain storage for both the `intnode` and the `doublenode` members. The use of a union allows the same storage to be used for both members.