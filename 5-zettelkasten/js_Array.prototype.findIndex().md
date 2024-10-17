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
#### Find the index of a prime number in an array
The following example returns the index of the first element in the array that is a prime number, or `-1` if there is no prime number.

```JavaScript title:app.js
function isPrime(element) {
  if (element % 2 === 0 || element < 2) {
    return false;
  }
  for (let factor = 3; factor <= Math.sqrt(element); factor += 2) {
    if (element % factor === 0) {
      return false;
    }
  }
  return true;
}

console.log([4, 6, 8, 9, 12].findIndex(isPrime)); // -1, not found
console.log([4, 6, 7, 9, 12].findIndex(isPrime)); // 2 (array[2] is 7)
```

#### Using the third argument of callbackFn
The `array` argument is useful if you want to access another element in the array, especially when you don’t have an existing variable that refers to the array. The following example first users `filter()` to extract the positive values and the uses `findIndex()` to find the first element that is less than its neighbors.

```JavaScript title:app.js
const numbers = [3, -1, 1, 4, 1, 5, 9, 2, 6];
const firstTrough = numbers
  .filter((num) => num > 0)
  .findIndex((num, idx, arr) => {
    // Without the arr argument, there's no way to easily access the
    // intermediate array without saving it to a variable.
    if (idx > 0 && num >= arr[idx - 1]) return false;
    if (idx < arr.length - 1 && num >= arr[idx + 1]) return false;
    return true;
  });
console.log(firstTrough); // 1
```

#### Using findIndex() on sparse arrays
You can search for `undefined` in a sparse array and get the index of an empty slot.

```JS title:app.js
console.log([1, , 3].findIndex((x) => x === undefined)); // 1
```

#### Calling findIndex() on non-array objects
The `findIndex()` method reads the `length` property of `this` and then accesses each property whose key is a non-negative integer less than `length`.

```JavaScript title:app.js
const arrayLike = {
  length: 3,
  "-1": 0.1, // ignored by findIndex() since -1 < 0
  0: 2,
  1: 7.3,
  2: 4,
};
console.log(
  Array.prototype.findIndex.call(arrayLike, (x) => !Number.isInteger(x)),
); // 1
```