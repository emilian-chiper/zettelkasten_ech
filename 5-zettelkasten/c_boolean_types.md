### Meta
2024-10-25 14:55
**Tags:** [[c]] [[c_objects_functions_types]] [[c_object_types]]
**Status:** #completed 

### Boolean Types
Objects declared as `_Bool` can store only the values `0` and `1`.

This *Boolean type* was introduced in C99, and starts with an underscore to differentiate it in existing programs that had already declared their own identifiers named `bool` or `boolean`.

Identifiers that begin with an underscore and either an uppercase letter or another underscore are always reserved.

If you include the header `<stdboo.h>`, you can also spell this type as `bool` and assign it the values `true` (which expands to the integer constant `1`) and `false` (which expands to the integer constant `0`).

Here we declare to Boolean variables using both spellings of the type name:
```C title:boolean_declarations.c
#include <stdbool.h>
_Bool flag1 = 0;
bool flag2 = false;
```

Both spellings still work, but it’s better to use `bool`, as this is the long-term direction for the language.