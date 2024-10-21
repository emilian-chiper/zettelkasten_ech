### Meta
2024-10-17 13:58
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const array1 = [5, 12, 8, 130, 44];

const isLargeNumber = (element) => element > 13;

console.log(array1.findIndex(isLargeNumber));
// Expected output: 3
```

### What it does
The `findIndex()` method of `Array` instances returns the index of the first element in an array that satisfies the provided testing function. Otherwise, it returns `-1`.

### Syntax

```JavaScript title:app.js
findIndex(callbackFn)
findIndex(callbackFn, thisArg)
```

#### Parameters
`callbackFn`
A function to execute for each element in the array. It should return a truthy value to indicate a matching element has been found, and a falsy value otherwise. The function is called with the following arguments:
	`element`
	The current element being processed in the array.
	`index`
	The index of the current element being processed in the array.
	`array`
	The array `findIndex()` was called upon.

`thisArg` (Optional)
A value to use as `this` when executing `callbackFn`.

#### Return value
The index of the first element in the array that passes the test. Otherwise, `-1`.

### Description.
The `findIndex()` method is an iterative method. It calls a provided `callbackFn` function once for each element in an array in ascending-index order, until `callbackFn` returns a truthy value. `findIndex()` then returns the index of that element and stops iterating through the array. If `callbackFn` never returns a truthy value, `findIndex()` returns `-1`.

`callbackFn` is invoked for *every* index of the array, not just those with assigned values. Empty slots in sparse arrays behave the same as `undefined`.

The `findIndex()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

### Examples
For more examples, see [Array.prototype.findIndex()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex#examples).