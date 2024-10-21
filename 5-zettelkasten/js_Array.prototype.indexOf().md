### Meta
2024-10-16 22:33
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

console.log(beasts.indexOf('bison'));
// Expected output: 1

// Start from index 2
console.log(beasts.indexOf('bison', 2));
// Expected output: 4

console.log(beasts.indexOf('giraffe'));
// Expected output: -1
```

### What it does
The `indexOf()` method of `Array` instances returns the first index at which a given element can be found in the array, or -1 if it’s not present.

### Syntax
```JavaScript title:app.js
indexOf(seachElement)
indexOf(searchElement, fromIndex)
```

#### Parameters
`searchElement`
	Element to locate in the array.

`fromIndex` (Optional)
Zero-based index at which to start searching, converted to an integer.
- Negative index counts back from the end of the array — if `-array.length <= fromIndex < 0`, `fromIndex + array.length` is used. Note, the array is still searched from front to back in this case.
- If `fromIndex < -array.length` or `fromIndex` is omitted, `0` is used, causing the entire array to be searched.
- If `fromIndex >= array.length`, the array is not searched and `-1` is returned.

#### Return value
The first index of `searchElement` in the array; `-1` if not found.

### Description
The `indexOf` method compares `searchElement` to elements of the array using strict equality (the same algorithm used by the `===` operator). `NaN` values are never compared as equal, so `indexOf()` always returns `-1` when `searchElement` is `NaN`.

The `indexOf()` method skips empty slots in sparse arrays.

The `indexOf()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

### Examples
For more examples, see [Array.prototype.indexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf#examples).