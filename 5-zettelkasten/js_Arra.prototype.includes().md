### Meta
2024-10-17 12:00
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const array1 = [1, 2, 3];

console.log(array1.includes(2));
// Expected output: true

const pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat'));
// Expected output: true

console.log(pets.includes('at'));
// Expected output: false
```

### What it does
The `includes()` method of `Array` instances determines whether an array includes a certain value among its entries, returning `true` or `false` as appropriate.

### Syntax
```JavaScript title:app.js
includes(searchElement);
includes(searchEleemnt, fromIndex)
```

#### Parameters
`searchElement`
The value to search for.

`fromIndex`
Zero-based index at which to start searching, converted to an integer.
-  - Negative index counts back from the end of the array — if `-array.length <= fromIndex < 0`, `fromIndex + array.length` is used. However, the array is still searched from front to back in this case.
- If `fromIndex < -array.length` or `fromIndex` is omitted, `0` is used, causing the entire array to be searched.
- If `fromIndex >= array.length`, the array is not searched and `false` is returned.

#### Return value
A boolean value which is `true` if the value `searchElement` is found within the array (or the part of the array indicated by the index `fromIndex`, if specified).

### Description
The `includes()` method compares `searchElement` to elements of the array using the [SameValueZero](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-samevaluezero)  algorithm. Values of zero are all considered to be equal, regardless of sign. (That is, `-0` is equal to `0`), but `false` is *not* considered to be the same as `0`. `NaN` can be correctly searched for.

When used on sparse arrays, the `includes()` method iterates empty slots as if they have value `undefined`.

The `includes()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

### Examples
For more examples, see [Array.prototype.includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes#examples).