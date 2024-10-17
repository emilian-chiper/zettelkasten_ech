### Meta
2024-10-17 17:23
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #pending 

### What it looks like
```JavaScript title:app.js
const array1 = [5, 12, 50, 130, 44];

const isLargeNumber = (element) => element > 45;

console.log(array1.findLastIndex(isLargeNumber));
// Expected output: 3
// Index of element with value: 130
```

### What it does
The `findLastIndex()` method of `Array` instances iterates the array in reverse order and returns the index of the first element that satisfies the provided testing function. If no elements satisfy the testing function, `-1` is returned.

### Syntax
```JS title:app.js
findLastIndex(callbackFn)
findLastIndex(callbackFn, thisArg)
```

#### Parameters
`callbackFn`
A function to execute for each element in the array. It should return a truthy value to indicate a matching element has been found, and a falsy value otherwise. The function is called with the following arguments:
	`element`
	The current element being processed in the array.
	`index`
	The index of the current element being processed in the array.
	`array`
	The array `findLastIndex()` was called upon.

`thisArg` (Optional)
A value to use as `this` when executing `callbackFn`.

#### Return value
The index of the last (highest-index) element in the array that passes the test. Otherwise, returns `-1`.

### Description
The `findLastIndex()` method is an iterative method. It calls a provided `callbackFn` function once for each element in an array in descending-index order, until `callbackFn` returns a truthy value. `findLastIndex()` then returns the index of that element and stops iterating through the array. If `callbackFn` never returns a truthy value, `-1` is returned.

`callbackFn` is invoked for *every* index of the array, not just those with assigned values. Empty slots in sparse arrays behave the same as `undefined`.

The `findLastIndex()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.