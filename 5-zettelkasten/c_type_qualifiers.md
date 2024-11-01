### Meta
2024-10-27 21:33
**Tags:** [[c]] [[c_objects_functions_types]]
**Status:** #completed 

### Type Qualifiers
Types can be *qualified* by using one or more of the following qualifiers: `const`, `volatile`, and `restrict`. Each of these qualifiers changes behaviors when accessing objects of the qualified type.

The qualified and unqualified versions of types can be used interchangeably as arguments to functions, return values from functions, and members of unions.

**Note:** The `_Atomic` qualifier, available since C11, supports concurrent programs.

#### const
Objects declared with the `const` qualifier (`const`-qualified types) are not modifiable. They’re not assignable but can have constant initializers. They can be placed in read-only memory by the compiler, and any attempt to write to them will result in a runtime error:

```C title:example.c
const int i = 1; // const-qualified int
i = 2; // error: i is const-qualified
```

It’s possible to accidentally convince your compiler to change a `const`-qualified object for you. In the following example, we take the address of a `const`-qualified object `i` and tell the compiler that this is actually a pointer to an `int`:

```C title:example.c
const int i = 1; // object of const-qualified type
int *ip = (int *)&i;
*ip = 2; // undefined behavior
```

C doesn’t allow you to cast away the `const` if the original was declared as a `const`-qualified object. This code might appear to work, but it’s defective and might fail later; e.g., the compiler might place the `const`-qualified object in read-only memory, causing a memory fault when trying to store a value in the object at runtime.

C allows you to modify an object that is pointed to by a `const`-qualified pointer by casting the const away, provided the original object was not declared `const`:

```C title:example.c
int i = 12;
const int j = 12;

const int *ip = &i;
const int *jp = &j;

*(int *)ip = 42; // ok
*(int *)jp = 42; // undefined behavior
```

#### volatile
Objects of `volatile`-qualified types serve a special purpose. Static `volatile`-qualified objects are used to model memory-mapped I/O ports, and static constant `volatile`-qualified objects model memory-mapped input ports such as a real-time clock.

The values stored in these objects may change without the knowledge of the compiler. e.g, each time the value of a real-time clock is read, it may change, even if the value has not been written to by the C program.

Using a `volatile`-qualified type lets the compiler know that the value may change, and esures that every access to the real-time clock occurs (otherwise, an access to the real-time clock may be optimized away or replaced by a previously read and cached value).

In the following code, the compiler must generate instructions to read the value from `port` and then write this value back to `port`:

```C title:example.c
volatile int port;
port = port;
```

Without the `volatile` qualification, the compiler would see this as a `no-op` (a programming statement that does nothing) and potentially eliminate both the read and the write.

Also, `volatile`-qualified types are used for communications with the `signal` handlers and with `setjmp/longjmp` (see C Standard). Unlike in Java 🤮 and other programming language, `volatile`-qualified types in C should not be used for synchronization between threads.

#### restrict
A `restrict`-qualified pointer is used to promote optimization.

Objects indirectly accessed through a pointer frequently cannot be fully optimized because of potential *aliasing*, which occurs when more than one pointer refers to the same object. Aliasing can inhibit optimizations, because the compiler can’t tell if portions of an object can change values when another apparently unrelated object is modified, for example.

The following function copies `n` bytes from the storage referenced by `q` to the storage referenced by `p`. The function parameters `p` and `q` are both `restrict`-qualified pointers.

```C title:example.c
void f(unsigned int n, int * restrict p, int * restrict q)
{
	while (n-- > 0) {
		*p++ = *q++;
	}
}
```

Because both `p` and `q` are `restrict`-qualified pointers, the compiler can assume that an object accessed through one of the pointer parameters is not also accessed through the other. The compiler can make this assessment based solely on the parameter declarations without analyzing the function body. Although using `restrict`-qualified pointers can result in more efficient code, you must ensure that the pointers do not refer to overlapping memory to prevent undefined behavior.