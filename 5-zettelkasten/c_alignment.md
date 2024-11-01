### Meta
2024-10-25 14:36
**Tags:** [[c]] [[c_objects_functions_types]]
**Status:** #completed 

### Alignment
Object types have alignment requirements that place restrictions on the addresses at which objects of that type may be allocated.

An *alignment* represents the number of bytes between successive addresses at which a given object can be allocated. CPUs may have different behavior when accessing aligned data (e.g., the data address is a multiple of the data size) versus unaligned data.

Some machine instructions can perform multibyte accesses on non-word boundaries, but there may be a performance penalty.

A word is a natural, fixed-sized unit of data handled by the instruction set or the hardware of the processor.

Some platforms cannot access unaligned memory. Alignment requirements may depend on the CPU word size (typically, 16, 32, or 64 bits).

Generally, C programmers need not concern themselves with alignment requirements, because the compiler chooses suitable alignments for its various types.

Dynamically allocated memory from `malloc` is required to be sufficiently aligned for all standard types, including arrays and structures.

On rare occasions, you might need to override the compiler’s default choices, e.g., to align data on the boundaries of the memory cache lines that must start at power-of-two address boundaries, or to meet other system-specific requirements. Traditionally, these requirements were met by linker commands, or by overallocating memory with `malloc` followed by rounding the user address upward, or similar operations involving other non-standard facilities.

C11 introduced a simple, forward-compatible mechanism for specifying alignments. Alignments are represented as values of the type `size_t`. Every valid alignment value is a nonnegative integral power of two. An object type imposes a default alignment requirement on every object of that type: a stricter alignment (a larger power of two) can be requested using the alignment specifier (`_Alignas`). You can include an alignment specifier in the declaration specifiers of a declaration.

Listing 2-7 uses the alignment specifier to ensure that `good_buff` is properly aligned (`bad-buff` may have incorrect alignment for member-access expressions).

*Listing 2-7: Use of the _Alignas keyword*
```C title:alignas.c
struct S {
	int i; double d; char c;
};

int main(void) {
	usigned char bad_buff[sizeof(struct S)];
	_Alignas(struct S) unsigned char good_buff[sizeof(struct S)];

struct S *bad_s_ptr = (struct S *)bad_buff; // wrong pointer alignmnet
struct S *good_s_ptr = (struct S *)good_buff; // correct pointer alignment
}
```

Alignments are ordered from weaker to stronger (aka stricter) alignments. Stricter alignments have larger alignment values. An address that satisfies an alignment requirement also satisfies any valid, weaker alignment requirements.