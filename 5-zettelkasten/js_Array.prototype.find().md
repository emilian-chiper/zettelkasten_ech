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
#### Find an object in an array by one of its properties
```JavaScript title:app.js
const inventory = [
  { name: "apples", quantity: 2 },
  { name: "bananas", quantity: 0 },
  { name: "cherries", quantity: 5 },
];

function isCherries(fruit) {
  return fruit.name === "cherries";
}

console.log(inventory.find(isCherries));
// { name: 'cherries', quantity: 5 }
```

#### Using arrow function and destructuring
```JavaScript title:app.js
const inventory = [
  { name: "apples", quantity: 2 },
  { name: "bananas", quantity: 0 },
  { name: "cherries", quantity: 5 },
];

const result = inventory.find(({ name }) => name === "cherries");

console.log(result); // { name: 'cherries', quantity: 5 }
```

#### Find a prime number in an array
The following example finds an element in the array that is a prime number (or returns `undefined` if there’s no such number):

```JavaScript title:app.js
function isPrime(element, index, array) {
  let start = 2;
  while (start <= Math.sqrt(element)) {
    if (element % start++ < 1) {
      return false;
    }
  }
  return element > 1;
}

console.log([4, 6, 8, 12].find(isPrime)); // undefined, not found
console.log([4, 5, 8, 12].find(isPrime)); // 5
```

#### Using the third argument of callbackFn
The `array` argument is useful if you want to access another element in the array, especially when you don’t have an existing variable that refers to the array. The following example firs uses `filter()` to extract the positive values and then uses `find()` to find the first element that is less than its neighbors.

```JavaScript title:app.js
const numbers = [3, -1, 1, 4, 1, 5, 9, 2, 6];
const firstTrough = numbers
  .filter((num) => num > 0)
  .find((num, idx, arr) => {
    // Without the arr argument, there's no way to easily access the
    // intermediate array without saving it to a variable.
    if (idx > 0 && num >= arr[idx - 1]) return false;
    if (idx < arr.length - 1 && num >= arr[idx + 1]) return false;
    return true;
  });
console.log(firstTrough); // 1
```

#### Using find() on sparse arrays
Empty slots in sparse arrays *are* visited, and are treated the same as `undefined`.

```JavaScript title:app.js
// Declare array with no elements at indexes 2, 3, and 4
const array = [0, 1, , , , 5, 6];

// Shows all indexes, not just those with assigned values
array.find((value, index) => {
  console.log("Visited index ", index, " with value ", value);
});
// Visited index 0 with value 0
// Visited index 1 with value 1
// Visited index 2 with value undefined
// Visited index 3 with value undefined
// Visited index 4 with value undefined
// Visited index 5 with value 5
// Visited index 6 with value 6

// Shows all indexes, including deleted
array.find((value, index) => {
  // Delete element 5 on first iteration
  if (index === 0) {
    console.log("Deleting array[5] with value", array[5]);
    delete array[5];
  }
  // Element 5 is still visited even though deleted
  console.log("Visited index", index, "with value", value);
});
// Deleting array[5] with value 5
// Visited index 0 with value 0
// Visited index 1 with value 1
// Visited index 2 with value undefined
// Visited index 3 with value undefined
// Visited index 4 with value undefined
// Visited index 5 with value undefined
// Visited index 6 with value 6
```

#### Calling find() on non-array objects
The `find()` method reads the `length` property of `this` and the accesses each property whose key is a non-negative integer less than `lenght`.

```JavaScript title:app.js
const arrayLike = {
  length: 3,
  "-1": 0.1, // ignored by find() since -1 < 0
  0: 2,
  1: 7.3,
  2: 4,
};
console.log(Array.prototype.find.call(arrayLike, (x) => !Number.isInteger(x)));
// 7.3
```