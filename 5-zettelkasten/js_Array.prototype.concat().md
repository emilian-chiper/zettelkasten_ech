### Meta
2024-10-16 20:48
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const array1 = ['a', 'b', 'c'];
const array2 = ['d', 'e', 'f'];
const array3 = array1.concat(array2);

console.log(array3);
// Expected output: Array ["a", "b", "c", "d", "e", "f"]
```

### What it does
The `concat()` method of `Array` instances is used to merge two or more arrays. This method doesn’t change the existing arrays, but instead returns a new array.

### Syntax
```JavaScript title:app.js
concat()
concat(value1)
concat(value1, value2)
concat(value1, value2, /* ..., */, valueN)
```

#### Parameters
`value1`, …, `valueN` (Optional)
Arrays and/or values to concatenate into a new array. If all `valueN` parameters are omitted, `concat` returns a shallow copy of the existing array on which it is called. See the description below for more details.

#### Return value
A new `Array` instance.

### Description
The `concat()` method creates a new array. The array will first be populated by the elements in the object on which it is called. Then, for each argument, its value will be concatenated into the array – for normal objects or primitives, the argument itself will become an element of the final array; for arrays or array-like objects with the property [[symbol.isConcatSpreadable|Symbol.isConcatSpreadable]] set to a truthy value, each element of the argument will be independently added to the final array. The `concat` method does not recurse into nested array arguments.

The `concat()` method is a copying method. It doesn’t alter `this` or any of the arrays provided as arguments but instead returns a shallow copy that contains the same elements as the ones from the original arrays.

The `concat()` method preserves empty slots if any of the source arrays is sparse.

The `concat()` method is generic. The `this` value is treated in the same way as the other arguments (except it will be converted to an object first), which means plain objects will be directly prepended to the resulting array, while array-like objects with truthy `[Symbol.isConcatSpreadable]` will be spread into the resulting array.

### Examples
For more examples, see [Array.prototype.concat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat#examples).