### Meta
2024-10-24 13:36
**Tags:** [[c]] [[c_objects_functions_types]]
**Status:** #completed 

### Objects, Functions, Types, and Pointers
An **object** is storage in which you can represent values.

Per the C Standard (ISO/IEC 9899:2018) an object is a “region of data storage in the execution environment, the contents of which can represent values”, with the added note, “when referenced, an object can be interpreted as having a particular type.”

A variable is an example of an object.

**Variables** have a declared **type** that tells you the kind of object its value represents, e.g. an object with type `int` contains an integer value. The type is important because the collection of bits that represent one type of object will likely have a different value if interpreted as a different type of object.

For example, the number 1 is represented in IEEE 754 (IEEE Standard for Floating-Point Arithmetic) by the bit pattern `0x3f800000` (IEEE 754-2008). If you were to interpret this same bit pattern as an integer, you’d get the value `1,065,353,216` instead of 1.

**Functions** are not objects but do have types. A function type is characterized by both its return type as well as the number and types of its parameters.

The C language also has **pointers**, which can be thought of as an **address** – a location in memory where an object or function is stored. A pointer type is derived from a function or object type called the **reference type**. A pointer type derived from the reference type `T` is called a *pointer* to `T`.

Because objects and functions are different things, object pointers and function pointers are also different things, and should not be used interchangeably.