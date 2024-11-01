### Meta
2024-10-28 08:38
**Tags:** [[c]] [[c_arithmetic_types]] [[c_integers]]
**Status:** #completed 

### The <limits.h> Header File
The `<limits.h>` header file provides the minimum and maximum representable values for the various integer types.

A *representable values* is one that can be represented in the number of bits available to an object of a particular type. Values that cannot be diagnosed by the compiler or converted to a representable but different (incorrect) value. Compiler writers provide the correct minimum, maximum, and width values for their implementations. To write portable code, you should use these constants, rather than integer literals such as `+2147483647` that represent a specific limit and may change when porting to a different implementation.

The C Standard imposes only three constraints on integer sizes:
- First, storage for *every* data type occupies an integral number of adjacent `unsigned char` objects (which may include padding).
- Second, each integer type has to support the minimum ranges, allowing you to depend on a portable range of values across any implementation.
- Third, smaller types cannot be wider than larger types; e.g., `USHRT_MAX` cannot be greater that `UINT_MAX`, but they can be the same width.