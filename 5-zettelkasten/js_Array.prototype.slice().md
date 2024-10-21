### Meta
2024-10-16 13:20
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// Expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// Expected output: Array ["camel", "duck"]

console.log(animals.slice(1, 5));
// Expected output: Array ["bison", "camel", "duck", "elephant"]

console.log(animals.slice(-2));
// Expected output: Array ["duck", "elephant"]

console.log(animals.slice(2, -1));
// Expected output: Array ["camel", "duck"]

console.log(animals.slice());
// Expected output: Array ["ant", "bison", "camel", "duck", "elephant"]
```

### What it does
The `slice()` method of `Array` instances returns a shallow copy of a portion of an array into a new array object selected form `start` to `end` (`end` not included) where `start` and `end` represent the index of the items in that array. The original array will not be modified.

### Syntax
```JavaScript title:app.js
slice()
slice(start)
slice(start, end)
```

#### Parameters
`start` (Optional)
Zero-based index at which to start execution, converted to an integer.
- Negative index counts back from the end of the array – if `-array.length <= start < 0`, `start + array.length` is used.
- If `start < -array.length` or `start` is omitted, `0` is used.
- If `start >= array.length`, an empty array is returned.

`end` (Optional)
Zero-based index at which to end extraction, converted to an integer. `slice()` extracts up to bu not including `end`.
- Negative index counts back from the end of the array – if `-array.length <= end < 0`, `end + array.length` is used.
- If `end < -array.length`, `0` is used.
- If `end >= array.length` or `end` is omitted, `array.length` is used, causing all elements until the end to be extracted.
- If `end` implies a position before or at the position that `start` implies, an empty array is returned.

#### Return value
A new array containing the extracted elements.

### Description
The `slice()` method is a copying method. It does not alter `this` but instead it returns a `shallw copy` that contains some of the same elements as the ones from the original array.

The `slice()` method preserves empty slots. If the slices portion is sparse, the returned array is sparse as well.

The `slice()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

### Examples
For more examples, see [Array.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice#examples).