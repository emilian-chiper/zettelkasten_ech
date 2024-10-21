### Meta
2024-10-17 11:49
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const animals = ['Dodo', 'Tiger', 'Penguin', 'Dodo'];

console.log(animals.lastIndexOf('Dodo'));
// Expected output: 3

console.log(animals.lastIndexOf('Tiger'));
// Expected output: 1
```

### What it does
The `lastIndexOf()` of `Array` instances returns the last index at which a given element can be found in the array, or `-1` if it’s not present. The array is searched backwards, starting at `fromIndex`.

### Syntax
```JavaScript title:app.js
lastIndexOf(searchElement)
lastIndexOf(searchElement, fromIndex)
```

#### Parameters
`searchElement`
Element to locate in the array.

`fromIndex` (Optional)
Zero-based index at which to start searching backwards, converted to an integer.
- - Negative index counts back from the end of the array — if `-array.length <= fromIndex < 0`, `fromIndex + array.length` is used.
- If `fromIndex < -array.length`, the array is not searched and `-1` is returned. You can think of it conceptually as starting at a nonexistent position before the beginning of the array and going backwards from there. There are no array elements on the way, so `searchElement` is never found.
- If `fromIndex >= array.length` or `fromIndex` is omitted, `array.length - 1` is used, causing the entire array to be searched. You can think of it conceptually as starting at a nonexistent position beyond the end of the array and going backwards from there. It eventually reaches the real end position of the array, at which point it starts searching backwards through the actual array elements.

#### Return value
The last index of `searchElement` in the array; `-1` if not found.

### Description
The `lastIndexOf()` method compares `searchElement` to elements of the array using strict equality (the same algorithm used by the `===` operator). `NaN` values are never compared as equal, so `lastIndexOf()` always returns `-1` when `searchElement` is `NaN`.

The `lastIndexOf()` method skips empty slots in sparse arrays.

The `lastIndexOf()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

### Examples
For more examples, see [Array.prototype.lastIndexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf#examples).