### Meta
2024-10-15 12:57
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const array1 = [1, 2, 3];

const firstElement = array1.shift();

console.log(array1); // Array [2, 3]

console.log(firstElement); // 1
```

### What it does
The `shift()` method of `Array` instances removes the **first** element from an array and returns that removed element. This method changes the length of the array.

### Syntax
```JavaScript title:app.js
shift()
```

#### Parameters
None.

#### Return value
The removed element form the array; `undefined` if the array is empty.

### Description
The `shift()` method removes the element at the zeroth index and shifts the values at consecutive indexes down, then returns the removed value. If the `lenght` property is 0, `undefined` is returned.

The `pop()` method has similar behavior to `shift()`, but applied to the last element in the array.

The `shift()` method is a mutating method. It changes the length and the content of `this`. In case you want the value of `this` to be the same, but return a new array with the first element removed, you can use `arr.slice(1)` instead.

The `shift()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties. Although strings are also array-like, this method is not suitable to be applied to them, as strings are immutable.

### Examples
For more examples see [Array.prototype.shift()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift#examples).