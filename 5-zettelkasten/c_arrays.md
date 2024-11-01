### Meta
2024-10-25 22:23
**Tags:** [[c]] [[c_objects_functions_types]] [[c_derived_types]]
**Status:** #completed 

### Arrays
An *array* is a contiguously allocated sequence of objects that all have the same element type.

Array types are characterized by their element types and the number of elements in the array. Here we declare an array of `11` elements of type `int` identified by `ia`, and an array of `17` elements of type pointer to `float` identified by `afp`:
```C title:array_declarations.c
int ia[11];
float *afp[17];
```

You use square brackets to identify an element of an array. For example, the following contrived code snippet creates the string `"0123456789"` to demonstrate how to assign values to the elements of an array:
```C title:arr.c
char str[11];
for (unsigned int i = 0; i < 10; ++i) {
	str[i] = '0' + i;
}
str[10] = '\0';
```

The first line declares an array of `char` with a bound of `11`. This allocates sufficient storage to create a string with 10 characters plus a null character. The `for` loop iterates 10 times, with the values of `i` ranging from `0` to `9`. Each iteration assigns the result of the expression `'0 + i` to `str[i]`. Following the end of the loop, the null character is copied to the final element of the array `str[10]`.

In the expression at line 3, `str` is automatically converted to a pointer to the first member of the array (an object of type `char`), and `i` has an unsigned integer type. The subscript (`[]`) operator and addition (`+`) operator are defined so that `str[i]` is identical to `(str + i)`. When `str` is an array object, the expression `str[i]` designates the ith element of the array (counting from 0). Because arrays are indexed starting from `0`, the array `str[11]` is indexed from `0` to `10`, with `10` being the last element, as referenced on the last line of this example.

If the operand of the unary `&` operator is the result of a `[]` operator, the result is as if the `&` operator were removed and the `[]` operator were changed to a `+` operator. For example `&str[10]` is the same as `str + 10`.

You can also declare multidimensional arrays. Listing 2-8 declares `arr` in the function `main` as a two-dimensional 5 x 3 array of type `int`, also referred to as a *matrix*.

*Listing 2-8: Matrix operations*
```C title:matrix_operations.c
void func(int arr[5]);

int main(void)
{
	unsigned int i = 0;
	unsigned int j = 0;
	int arr[3][5];
	func(arr[i]);
	int x = arr[i][j];
	return 0;
}
```

More precisely, `arr` is an array of three elements, each of which is an array of five elements of type `int`. When you use the expression `arr[i]` (equivalent to `*(arr+i)`), the following occurs:
1. `arr` is converted to a pointer to the initial array of five elements of type `int` starting at `arr[i]`.
2. `i` is scaled to the type of `arr` by multiplying `i` by the size of one array of five `int` objects.
3. The results from steps 1 and 2 are added.
4. Indirection is applied to the result to produce an array of five elements of type `int`.

When used in the expression `arr[i][j]`, that array is converted to a pointer to the first element of type `int`, so `arr[i][j]` produces an object of type `int`.