### Meta
2024-10-20 21:21
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #pending 

### What it looks like
```JavaScript title:app.js
const array1 = [
	[0, 1],
	[2, 3],
	[4, 5],
];

const result = array1.reduceRight((accumulator, currentValue) =>
  accumulator.concat(currentValue),
);

console.log(result);
// Expected output: Array [4, 5, 2, 3, 0, 1]
```

### What it does
The `reduceRight()` method of `Array` instances applies a function against an accumulator and each value of the array (from right-to-left) to reduce it to a single value.

### Syntax
```JavaScript title:app.js
reduceRight(callbackFn)
reduceRight(callbackFn, initialValue)
```

#### Parameters
`callbackFn`
	A function to execute for each element in the array. Its return value becomes the value of the `accumulator` parameter on the next invocation of `callbackFn`. For the last invocation, the return value becomes the return value of `reduceRigh()`. The function is called with the following arguments:
	`accumulator`
		The value resulting from the previous call to `callbackFn`. On the first call, its value is `initialValue` if the latter is specified; otherwise its value is the last element of the array.
	`currentValue`
		The value of the current element. On the first call, its value is the last element if `initialValue` is specified; otherwise its value is the second to last element.
	`currentIndex`
		The index position of `currentValue` in the array. On the first call, its value is `array.length - 1` if `initialValue` is specified, otherwise `array.length - 2`.
	`array`
		The array `reduceRight()` was called upon.

`initialValue` (Optional)
	Value to use as accumulator to the first call of the `callbackFn`. If no initial value is supplied, the last element in the array will be used and skipped. Calling `reduceRight()` on an empty array without an initial value creates `TypeError`.

#### Return value
The value that results from the reduction.

### Description
The `reduceRight()` method is an iterative method. It runs a “reducer” callback function over all elements in the array, in descending-index order, and accumulates them into a single value. Read the iterative methods section for more information about how these methods work in general.

`callbackFn` is invoked only for the array indexes which have assigned values. It is not invoked for empty slots in sparse arrays.

Unlike other iterative methods, `reduceRight()` does not accept a `thisArg` argument. `callbackFn` is always called with `undefined` as `this`, which gets substituted with `globalThis` if `callbackFn` is non-strict.

The `reduceRight()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

All caveats about `reduce` discussed in [when to not use reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#when_to_not_use_reduce) apply to `reduceRight` as well. Because JavaScript has no lazy evaluation semantics, there is no performance difference between `reduce` and `reduceRight`.

### Examples
For further examples, see [Array.prototype.reduceRight()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight#examples).