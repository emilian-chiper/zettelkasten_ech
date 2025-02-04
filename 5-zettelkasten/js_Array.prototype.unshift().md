### Meta
2024-10-15 13:07
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const array1 = [1, 2, 3];

console.log(array1.unshift(4, 5)); // 5

console.log(array1); // Array [4, 5, 1, 2, 3]
```

### What it does
The `unshift()` method of `Array` instances adds the specified elements to the beginning of an array and returns the new length of the array.

### Syntax
```JavaScript title:app.js
unshift()
unshift(element1)
unshift(element1, element2)
unshift(element1, element2, /* …, */ elementN)
```

#### Parameters
`element1`, …, `elementN`
	The elements to add to the front of the `arr`.

#### Return value
The new `length` property of the object upon which the method was called.

### Description
The `unshift()` method inserts the given values to the beginning of an array-like object.

`Array.prototype.psuh()` has a similar behavior to `unshift()`, but applied to the end of the array.

Please note that, if multiple elements are passed as parameters, they’re inserted in chunk at the beginning of the object, in the exact same order they were passed as parameters. Hence, calling `unshift()` with `n` arguments **once**, or calling it `n` times with **1** argument (with a loop, for example), don’t yield the same result.

```JavaScript title:app.js
let arr = [4, 5, 6];

arr.unshift(1, 2, 3);
console.log(arr);
// [1, 2, 3, 4, 5, 6]

arr = [4, 5, 6]; // resetting the array

arr.unshift(1);
arr.unshift(2);
arr.unshift(3);

console.log(arr);
// [3, 2, 1, 4, 5, 6]
```

The `unshift()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties. Although strings are also array-like, this method is not suitable to be applied on them, as strings are immutable.

### Examples
For more examples, see [Array.prototype.unshift()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift#examples).