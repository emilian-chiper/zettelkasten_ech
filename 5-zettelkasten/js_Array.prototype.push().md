### Meta
2024-10-14 13:39
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const animals = ['pigs', 'goats', 'sheep'];

const count = animals.push('cows');
console.log(count); // 4
```

### What it does
The `push()` method of `Array` instances adds the specified elements to the end of an array and returns the new length of the array.

### Syntax
```JavaScript title:app.js
push()
push(element1)
push(element1, element2)
push(element1, element2, /* …, */ elementN)
```

#### Parameters
`element1`, …, `elementN`
	The element(s) to add to the end of the array.

#### Return value
The new `lenght` property of the object upon which the method was called.

### Description
The `push` method appends values to an array.

The `push` method is a *mutating* method. It changes the length and the content of `this`. In case you want the value of `this` to be the same, but return a new array with elements appended to the end, you can use [[js_Array.prototype.concat()|`arr.concat([el0, el1, ..., elN])`]] instead. Notice that the elements are wrapped in an extra array. Otherwise, if the element is an array itself, it would be spread instead of pushed as single element due to the behavior of `concat()`.

The `push` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties. Although strings are also array-like, this method is not suitable to be applied on them, as strings are immutable.

### Examples
For more examples, see [Array.prototype.push()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push#examples).