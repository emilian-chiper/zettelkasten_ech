### Meta
2024-10-17 12:40
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed

### What it looks like
```JavaScript title:app.js
const array1 = [5, 12, 8, 130, 44];

const found = array1.find((element) => element > 10);

console.log(found);
// Expected output: 12
```

### What it does
The `find()` method of `Array` instances returns the first element in the provided array that satisfies the provided testing function. If no values satisfy the testing function, it returns `undefined`.
- If you need the **index** of the found element in the array, use [[js_Array.findIndex()|findIndex()]].
- If you need to find the **index of a value**, use [[js_Array.prototype.indexOf()|indexOf()]].
- If you need to find if a value **exists** in an array, use [[js_Arra.prototype.includes()|includes()]].
- If you need to find if any element satisfies the provided testing function, use [[js_Array.prototype.some()|some()]].
- If you need to find all elements that satisfy the provided testing function, use [[js_Array.prototype.filter()|filter()]].

### Syntax
```JavaScript title:app.js
find(callbackFn)
find(callbackFn, thisArg)
```

#### Parameters
`callbackFn`
A function to execute for each element in the array. It should return a truthy value indicating that a matching element has been found, and a falsy value otherwise. The function is called with the following arguments:
	`element`
	The current element being processed in the array.
	`index`
	The index of the current element being processed in the array.
	`array`
	The array `find()` was called upon.

`thisArg` (Optional)
A value to use as `this` when executing `callbackFn`.

#### Return value
The first element in the array that satisfies the provided testing function. Otherwise, `undefined`.

### Description
The `find()` method is an iterative method. It calls a provided `callbackFn` function once for each element in an array in ascending-index order, until `callbackFn` returns a truthy value. `find()` then returns that element and stops iterating through the array. If `callbackFn` never returns a truthy value, `find()` returns `undefined`.

`callbackFn` is invoked for *every* index of the array, not just those with assigned values. Empty slots in sparse arrays behave the same as `undefined`.

The `find()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

### Examples
For more examples, see [Array.prototype.find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find#examples).