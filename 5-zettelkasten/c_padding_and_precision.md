### Meta
2024-10-28 08:35
**Tags:** [[c]] [[c_arithmetic_types]] [[c_integers]]
**Status:** #completed 

### Padding and Precision
All integer types except `char`, `signed char`, and `unsigned char` may contain unused bits, called *padding*, that allow implementations to accommodate hardware quirks (such as skipping over a sign bit in the middle of a multiple-word representation), or to optimally align with a target architecture. The number of bits used to represent a value of a given type, excluding padding but including the sign, is called the *width* and is often denoted by *N*. The *precision* is the number of bits used to represent values, excluding sign and padding bits.