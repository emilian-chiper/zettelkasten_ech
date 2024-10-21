### Meta
2024-10-20 20:46
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// Expected outpup: "Fire,Air,Water"

console.log(elements.join());
// Expected output: "FireAirWater"

console.log(elements.join('-'));
// Expected output: "Fire-Air-Water"
```

### What it does
The `join()` method of `Array` instances creates and returns a new string by concatenating all of the elements in this array, separated by commas or a specified separator string. If the array has only one item, then that item will be returned without using the separator.

### Syntax
```JavaScript title:app.js
join()
join(separator)
```

#### Parameters
`separator` (Optional)
	A string to separate each pair of adjacent elements of the array. If omitted, the array elements are separated with a comma (“,”).

#### Return value
A string with all array elements joined. If `array.length` is `0`, the empty string is returned.

### Description
The string conversions of all array elements are joined into one string. If an element is `undefined` or `null`, it is converted to an empty string instead of the string `"null"` or `"undefined"`.

The `join` method is accessed internally by [[js_Array.prototype.toString()|Array.prototype.toString()]] with no arguments. Overriding `join` of an array instance will override its `toString` behavior as well.

`Array.prototype.join` recursively converts each element, including other arrays, to strings. Because the string returned by `Array.prototype.toString` (which is the same as calling `join()`) does not have delimiters, nested arrays look like they are flattened. You can only control the separator of the first level, while deeper levels always use default comma.

```JavaScript title:app.js
const matrix = [
	[1, 2, 3],
	[4, 5, 6],
	[7, 8, 9],
];

console.log(matrix.join()); // 1,2,3,4,5,6,7,8,9
console.log(matrix.join(';')); // 1,2,3;4,5,6;7,8,9
```

When an array is cyclic (it contains an element that is itself), browsers avoid infinite recursion by ignoring the cyclic reference.

```JavaScript title:app.js
const arr = [];
arr.push(1, [3, arr, 4], 2);
console.log(arr.join(";")); // 1;3,,4;2
```

When used on sparse arrays, the `join()` method iterates empty slots as if they have the value `undefined`.

The `join()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

### Examples
For more examples, see [Array.prototype.join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join#examples).