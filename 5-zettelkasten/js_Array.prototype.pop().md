### Meta
2024-10-15 12:44
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const plants = ['broccoli', 'cauliflower', 'cabbage', 'kale', 'tomato'];

console.log(plants.pop()); // "tomato"
```

### What it does
The `pop()` method of `Array` instances removes the **last** element from an array and returns that element. This method changes the length of the array.

### Syntax
```JavaScript title:app.js
pop()
```

#### Parameters
None.

#### Return value
The removed element from the array; `undefined` if the array is empty.

### Description
The `pop()` method removes the last element from an array and returns that value to the caller. If you call `pop()` on an empty array, it returns `undefined`.

[[js_Array.prototype.shift()|Array.prototype.shift()]] has similar behavior to `pop()`, but applied to the first element in an array.

The `pop()` method is a mutating method. It changes the length and the content of `this`. In case you want the value of `this` to be the same, but return a new array with the last element removed, you can use [[js_Array.prototype.slice()|arr.slice(0, -1)]] instead.

The `pop()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties. Although strings are also array-like, this method is not suitable to be applied on them, as strings are immutable.

### Examples
For more examples see [Array.prototype.pop()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop#examples).