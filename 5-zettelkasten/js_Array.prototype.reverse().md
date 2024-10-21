### Meta
2024-10-20 12:38
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #pending 

### What it looks like
```JavaScript title:app.js
const array1 = ['one', 'two', 'three'];
console.log('array1:', array1);
// Expected output: "array1:" Array ["one", "two", "three"]

const reversed = array1.reverse();
console.log('reversed:', reversed);
// Expected output: "reversed:" Array ["three", "two", "one"]

// Careful: reverse is destructive -- it changes the original array
console.log('array1:', array1);
// Expected output: "reversed:" Array ["three", "two", "one"]
```

### What it does
The `reverse()` method of `Array`  instances reverses an array in place and returns the reference to the same array, the first array element now becoming the last, and the last  array element becoming the first. In other words, elements order in the array will be turned towards the direction opposite to that previously stated.

To reverse the elements in an array without mutating the original array, use `toReversed()`.

### Syntax
```JS title:app.js
reverse()
```

#### Parameters
None.

#### Return value
The reference to the original array, now reversed. Note that the array is reversed in place, and no copy is made.

### Description
The `reverse()` method transposes the elements of the calling array object in place, mutating the array, and returning a reference to the array.

The `reverse()` method preserves empty slots. If the source array is sparse, the empty slots’ corresponding new indices are deleted and also become empty slots.

The `reverse()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties. Although strings are also array-like, this method is not suitable to be applied on them, as strings are immutable.

### Examples
For more examples, see [Array.prototype.reverse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse#examples).