### Meta
2024-10-20 21:00
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const array1 = [1, 2, 3, 4];

// 0 + 1 + 2 + 3 + 4
const initialValue = 0;
const sumtWithInitial = array1.reduce(
	(accumulator, currentValue) => accumulator + currentValue,
	initialValue,
);

console.log(sumWithInitial);
// Expected output: 10
```

### What it does
The `reduce()` method of `Array` instances executes a user-supplied “reducer” callback function on each element of the array, in order, passing in the return value from the calculation on the preceding element. The final result of running the reducer across all elements of the array is a single value.

The first time that the callback is run there is no “return value of the previous calculation”. If supplied, an initial value may be used in its place. Otherwise the array element at index 0 is used as the initial value and iteration starts from the next element (index 1 instead of index 0).

### Syntax
```JS title:app.js
reduce(callbackFn)
reduce(callbackFn, initialValue)
```

#### Parameters
`callbackFn`
A function to execute for each element in the array. Its return value becomes the value of the `accumulator` parameter on the next invocation of `callbackFn`. For the last invocation, the return value becomes the return value of `reduce()`. The function is called with the following arguments:
	`accumulator`
		The value resulting from the previous call to `callbackFn`. On the first call, its value is `initialValue` if the latter is specified; otherwise its value is `array[0]`.
	`currentValue`
		The value of the current element. On the first call, its value is `array[0]` if `initialValue` is specified; otherwise its value is `array[1]`.
	`currentIndex`
		The index position of the `currentValue` in the array. On the first call, its value is `0` if `initialValue` is specified, otherwise `1`.
	`array`
		The array `reduce()` was called upon.

`initialValue` (Optional)
	A value to which `accumulator` is initialized the first time the callback is called. If `initialValue` is specified, `callbackFn` starts executing with the first value in the array as `currentValue`. If `initialValue` is *not* specified, `accumulator` is initialized to the first value in the array, and `callbackFn` starts executing with the second value in the array as `currentValue`. In this case, if the array is empty (so that there’s no first value to return as `accumulator`), an error is thrown.

#### Return value
The value that results from running the “reducer” callback function to completion over the entire array.

#### Exceptions
`TypeError`
	Thrown if the array contains no elements and `initialValue` is not provided.

### Description
The `reduce()` method is an iterative method. It runs a “reducer” callback function over all elements in the array, in ascending-index order, and accumulates them into a single value. Every time, the return value of `callbackFn` is passed into `callbackFn` again on next invocation as `accumulator`. The final value of `accumulator` (which is the value returned from `callbackFn` on the final iteration of the array) becomes the return value of `reduce()`.

`callbackFn` is invoked only for array indexes which have assigned values. It is not invoked for empty slots in sparse arrays.

Unlike the other iterative methods, `reduce()` does not accept a `thisArg` argument. `callbackFn` is always called with `undefined` as `this`, which gets substituted with `globalThis` if `callbackFn` is non-strict.

`recuce()` is a central concept in functional programming, where it’s not possible to mutate any value, so in order to accumulate all values in an array, one must return a new accumulator value on every iteration. This convention propagates to JavaScript’s `reduce()`: you should use spreading or other copying methods where possible to create new arrays and objects as the accumulator, rather than mutating the existing one. If you decided to mutate the accumulator instead of copying it, remember to still return the modified object in the callback, or the next iteration will receive `undefined`. However, not that copying the accumulator may in turn lead to increased memory usage and degraded performance – see [When to not use reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#when_to_not_use_reduce). In such cases, to avoid bad performance and unreadable code, it’s better to use a simple `for` loop instead.

The `reduce()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

#### Edge cases
If the array only has one element (regardless of position) and no `initialValue` is provided, or if `intialValue` is provided but the array is empty, the solo value will be returned *without* calling `callbackFn`.

If `intialValue` is provided and the array is not empty, then the reduce method will always invoke the callback function starting at index 0.

If `initialValue` is not provided then the reduce method will act differently for arrays with length larger than 1, equal to 1 and 0, as shown in the following example:

```JavaScript title:app.js
const getMax = (a, b) => Math.max(a, b);

// callback is invoked for each element in the array starting at index 0
[1, 100].reduce(getMax, 50); // 100
[50].reduce(getMax, 10); // 50

// callback is invoked once for element at index 1
[1, 100].reduce(getMax); // 100

// callback is not invoked
[50].reduce(getMax); // 50
[].reduce(getMax, 1); // 1

[].reduce(getMax); // TypeError
```

### Examples
For more examples, see [Array.prototype.reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#examples).