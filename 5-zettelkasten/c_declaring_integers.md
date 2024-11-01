### Meta
2024-10-28 08:46
**Tags:** [[c]] [[c_arithmetic_types]] [[c_integers]]
**Status:** #pending 

### Declaring Integers
Unless explicitly declared as `unsigned`, integer types are assumed to be signed (except for `char`, which the implementation can define as either a signed or unsigned integer type). The following are valid declarations of unsigned integers:

```C title:example.c
usnigned int ui; // unsigned is required
unsigned u; // int can be omitted
unsigned long long ull2; // int can be omitted
unsigned char uc; // unsigned is required
```

When declaring signed integer types, you can omit the `signed` keyword–except for `signed char`, which requires the keyword to distinguish `signed char` from plain `char`.

Unless it is the only keyword present, `int` can also be omitted. For example, instead of declaring a variable to be of type `signed long long int`, it is common practice to just declare it as a `long long` and save some typing. The following are valid declarations of signed integers:

```C title:example.c
int i; // signed can be omitted
long long int sll; // signed can be omitted
long long sll2; // signed and int can be omitted
signed char sc; // signed is required
```