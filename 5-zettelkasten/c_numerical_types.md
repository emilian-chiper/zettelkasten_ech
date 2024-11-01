### Meta
2024-10-25 15:06
**Tags:** [[c]] [[c_objects_functions_types]] [[c_object_types]]
**Status:** #completed 

### Numerical Types
C provides several *numerical types* that can be used to represent integers, enumerators, and floating-point values.

#### Integer Types
*Signed integer types* can be used to represent negative numbers, positive numbers, and zero.

The signed integer types include `signed char`, `short int`, `int`, `long int` and `long long int`.

Except for `int` itself, the keyword `int` may be omitted in the declarations of these types, so you might, for example, declare a type by using `long long` instead of `long long int`.

For each signed integer type, there are corresponding *unsigned integer types* that use the same amount of storage: `unsigned char`, `unsigned short int`, `unsigned int`, `unsigned long int`, and `unsigned long long int`. These can be used to represent only positive numbers and zero.

The signed and unsigned integer types are used to represent integers of various sizes. Each platform determines the size for each of these types, given some constraints.

Each type has a minimum representable range. The types are ordered by width, guaranteeing that *wider* types are at least as large as *narrower* types so that an object of type `long long int` can represent all values that an object of type `long int`can represent, an object of type `long int` can represent all values that can be represented by an object of type `int`, etc.

The actual size of the various integer types can be inferred from the minimum and maximum representable values for the various integer types specified in the `<limits.h>` header file.

The `int` type usually has the natural size suggested by the architecture of the execution environment, so the size would be 16 bits wide on a 16-bit architecture, and 32 bits wide on a 32-bit architecture.

You can specify the actual-width integers by using type definitions from `<stdint.h>` or `<inttypes.h>` headers, like `uint32_t`. These headers also provide type definitions for the widest available integer types: `uintmax_t` and `intmax_t`.

#### enum Types
An *enumeration*, or `enum`, allows you to define a type that assigns names (*enumerators*) to integer values in cases with an enumerable set of constant values. The following are examples of enumerations:

```C title:enums.c
enum day { sun, mon, tue, wed, thu, fri, sat };
enum cardinal_points{ north = 0, east = 90, south = 180, west = 270 };
enum months { jan = 1, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec };
```

If you don’t specify a value to the first enumerator with the `=` operator, the value of its enumeration constant is `0`, and each subsequent enumerator without an `=` adds `1` to the value of the previous enumeration constant. Consequently, the value of `sun` in the `dau` enumeration is `0`, `mon` is `1`, etc.

You can also assign specific values to each enumerator, as shown by the `cardinal_points` enumeration. Using `=` with enumerators may produce enumeration constants with duplicate values, which can be a problem if you incorrectly assume all the values are unique.

The `months` enumeration sets the first enumerator at `1`, and each subsequent enumerator that isn’t specifically assigned a value will be incremented by `1`.

The actual value of the enumeration constant must be representable as an `int`, but its type is implementation defined; e.g., C++ uses a `signed int`, GCC uses an `unsigned int`.

#### Floating-Point Types
The C language supports three *floating-point types*: `float`, `double`, and `long double`.

Floating-point arithmetic is similar to, and often uses as a model for, the arithmetic of real numbers.