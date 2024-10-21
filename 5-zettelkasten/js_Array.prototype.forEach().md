### Meta
2024-10-16 21:07
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const array = ['a', 'b', 'c'];

array1.forEach((element) => console.log(element));

// Expected output: "a"
// Expected output: "b"
// Expected output: "c"
```

### What it does
The `forEach()` method `Array` instances executes a provided function once for each array element.

### Syntax
```JS title:app.js
forEach(callbackFn)
forEach(callbackFn, thisArg)
```

#### Parameters
`callbackFn`
A function to execute for each element in the array. Its return value is discarded. The function is called with the following arguments:
	`elements`
		The current element being processed in the array.
	`index`
		The index of the current element being processed in the array.
	`array`
		The array `forEach()` was called upon.

`thisArg` (Optional)
A value to use as `this` when executing `callbackFn`.

#### Return value
None (`undefined`).

### Description
The `forEach()` method is an iterative method. It calls a provided `callbackFn` function once for each element in an array is ascending-index order. Unlike `map()`, `forEach()` always returns `undefined` and is not chainable. The typical use case is to execute side effects at the end of a chain. Read the iterative methods section for more information about how these methods work in general.

`callbackFn` is invoked only for array indexes which have assigned values. It is not invoked for empty slots in sparse arrays.

The `forEach` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

There is no way to stop or break a `forEach()` loop other than by throwing an exception. If you need such behavior, the `forEach()` method is the wrong tool.

Early termination may be accomplished with looping statements like `for`, `for..of`, and `for..in`. Array methods like `every()`, `some()`, `find()`, and `findIndex()` also stops iteration immediately when further iteration is not necessary.

`forEach()` expects a synchronous function – it does not wait for promises. Make sure you are aware of the implications while using promises (or async functions) as `forEach` callbacks.

```JavaScript title:app.js
const ratings = [5, 4, 5];
let sum = 0;

const sumFunction = async (a, b) => a + b;

ratings.forEach(async (rating) => {
  sum = await sumFunction(sum, rating);
});

console.log(sum);
// Naively expected output: 14
// Actual output: 0
```

To run a series of asynchronous operations sequentially or concurrently, see [[js_using_promises|promise composition]].

### Examples
For more examples, see [Array.prototype.forEach()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#examples).