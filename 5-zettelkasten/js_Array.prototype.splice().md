### Meta
2024-10-16 12:48
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// Inserts at index 1
console.log(months);
// Expected output: Array ["Jan", "Feb", "March", "April", "June"]

months.splice(4, 1, 'May');
// Replaces 1 element at index 4
console.log(months);
// Expected output: Array ["Jan", "Feb", "March", "April", "May"]
```

### What it does
The `splice()` method of `Array` instances changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.

To create a new array with a segment removed and/or replace without mutating the original array, use [[js_Array.prototype.toSpliced()|toSpliced()]]. To access part of an array without modifying it, see [[js_Array.prototype.slice()|slice()]].

### Syntax
```JavaScript title:app.js
splice(start)
splice(start, deleteCount)
splice(start, deleteCount, item1)
splice(start, deleteCount, item1, item2, /* ..., */ itemN)
```

#### Parameters
`start`
Zero-based index at which to start changing the array, converted to an integer.
- Negative index counts back from the end of the array – if `-array.length <= start < 0`, `start + array.length` is used.
- If `start < -array.length`, `0` is used.
- If `start >= array.length`, no element will be deleted, but the method will behave as an adding function, adding as many elements as provided. 
- If `start` is omitted (and `splice()` is called with no arguments) nothing is deleted. This is different from passing `undefined`, which is converted to `0`.

`deleteCount`
An integer indicating the number of elements in the array to remove from `start`.

If `deletecount` is omitted, or if its value is greater than or equal to the number of elements after the positions specified by `start`, then all the elements from `start` to the end of the array will be deleted. However, if you wish to pass any `itemN` parameter, you should pass `Infinity` as `deleteCount` to delete all elements after `start`, because an explicit `undefined` gets converted to `0`.

If `deleteCount` is `0` or negative, no elements are removed. In this case, you should specify at least one new element (see below).

`item1`, …, `itemN` (Optional)
The elements to add to the array, beginning from `start`.

If you do not specify any elements, `splice` will only remove elements from the array.

#### Return value
An array containing the deleted elements.
If only one element is removed, an array of one element is returned.
If no elements are removed, an empty array is returned.

### Description
The `splice()` method is a mutating method. It may change the content of `this`. If the specified number of elements to insert differs form the number of elements being removed, the array’s `length` will be changed as well. At the same time, it uses [[js_symbol.species|Symbol.species]] to create a new array instance to be returned.

If the deleted portion is sparse (contains “empty slots”), the array returned by `splice` is sparse as well, with those corresponding indices being empty slots.

The `splice` method is generic. It only expects the `this`  value to have a `length` property and integer-keyed properties. Although strings are also array-like, this method is not suitable to be applied on them, as strings are immutable.

### Examples
For more examples, see [Array.prototype.splice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice#examples).