### Meta
2024-10-25 15:01
**Tags:** [[c]] [[c_objects_functions_types]] [[c_object_types]]
**Status:** #completed 

### Character Types
The C language defines the *character* types: `char`, `signed char`, and `unsigned char`.

Each compiler implementation will defined `char` to have the same alignment, size, range, representation, and behavior as either `signed char` or `unsigned char`. Regardless, `char` is a separate type from the other two and is incompatible with both.

The `char` type is used to represent character data in C language programs. Objects of type `char` must be able to represent the minimum set of characters required in the execution environment (aka the *basic execution character set*), including upper- and lowercase letters, the 10 decimal digits, the space character, and various punctuation and control characters.

The `char` type is inappropriate for integer data; it is safer to use `signed char` to represent small signed integer values, and `unsigned char` to represent small unsigned values.

The basic execution character set doesn’t include non-English letters. You can represent the characters of a large character set as *wide characters* by using the `wchar_t`, which takes more space than a basic character. Implementations choose 16 or 32 bits to represent a wide character.

The C Standard Library provides functions that support both narrow and wide character types.