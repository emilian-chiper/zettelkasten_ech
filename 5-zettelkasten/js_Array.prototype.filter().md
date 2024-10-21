### Meta
2024-10-18 13:26
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const words = ['spray', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter((word) => word.length > 6);

console.log(result);
// Expected output: Array ["exuberant", "destruction", "present"]
```

### What it does
The `filter()` method of `Array` instances creates a shallow copy of a portion of a given array, filtered down to just the elements from the given array that pass the test implemented by the provided function.

### Sytnax
```JS title:app.js
filter(callbackFn)
filter(callbackFn, thisArg)
```

#### Parameters
`callbackFn`
A function to execute for each element in the array. It should return a truthy value to keep the element in the resulting array, and a falsy value otherwise. The function is called with the following arguments.
	`element`
	The current element being processed in the array.
	`index`
	The index of the current element being processed in the array.
	`array`
	The array `filter()` was called upon.

`thisArg` (Optional)
A value to use as `this` when executing `callbackFn`.

#### Return value
A shallow copy of the given array containing just the elements that pass the test. If no elements pass the test, an empty array is returned.

### Description
The `filter()` method is an iterative method. It calls a provided `callbackFn` function once for each element in an array, and constructs a new array of all the values for which `callbackFn` returns a truthy value. Array elements which do not pass the `callbackFn` test are not included in the new array.

`callbackFn` is invoked only for array indexes which have assigned values. It is not invoked for empty slots in sparse arrays.

The `filter()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

### Examples
For more examples, see [Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter#examples).