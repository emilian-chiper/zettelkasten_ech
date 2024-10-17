### Meta
2024-10-16 13:20
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// Expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// Expected output: Array ["camel", "duck"]

console.log(animals.slice(1, 5));
// Expected output: Array ["bison", "camel", "duck", "elephant"]

console.log(animals.slice(-2));
// Expected output: Array ["duck", "elephant"]

console.log(animals.slice(2, -1));
// Expected output: Array ["camel", "duck"]

console.log(animals.slice());
// Expected output: Array ["ant", "bison", "camel", "duck", "elephant"]
```

### What it does
The `slice()` method of `Array` instances returns a shallow copy of a portion of an array into a new array object selected form `start` to `end` (`end` not included) where `start` and `end` represent the index of the items in that array. The original array will not be modified.

### Syntax
```JavaScript title:app.js
slice()
slice(start)
slice(start, end)
```

#### Parameters
`start` (Optional)
Zero-based index at which to start execution, converted to an integer.
- Negative index counts back from the end of the array – if `-array.length <= start < 0`, `start + array.length` is used.
- If `start < -array.length` or `start` is omitted, `0` is used.
- If `start >= array.length`, an empty array is returned.

`end` (Optional)
Zero-based index at which to end extraction, converted to an integer. `slice()` extracts up to bu not including `end`.
- Negative index counts back from the end of the array – if `-array.length <= end < 0`, `end + array.length` is used.
- If `end < -array.length`, `0` is used.
- If `end >= array.length` or `end` is omitted, `array.length` is used, causing all elements until the end to be extracted.
- If `end` implies a position before or at the position that `start` implies, an empty array is returned.

#### Return value
A new array containing the extracted elements.

### Description
The `slice()` method is a copying method. It does not alter `this` but instead it returns a `shallw copy` that contains some of the same elements as the ones from the original array.

The `slice()` method preserves empty slots. If the slices portion is sparse, the returned array is sparse as well.

The `slice()` method is generic. It only expects the `this` value to have a `length` property and integer-keyed properties.

### Examples
#### Return a portion of an existing array
```JavaScript title:app.js
const fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
const citrus = fruits.slice(1, 3);

// fruits contains ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
// citrus contains ['Orange','Lemon']
```

In this example, `slice(1, 3)` extracts elements from index `1` up to, but not including, index `3`, resulting in a new array `['Orange', 'Lemon']`.

#### Omitting the end parameter
```JavaScript title:app.js
const fruits = ["Apple", "Banana", "Orange", "Mango", "Pineapple"];

const tropical = fruits.slice(2);
console.log(tropical); // ['Orange', 'Mango', 'Pineapple']
```

In this example, `slice(2)` extracts elements from index `2` to the end of the array.

#### Using negative indices
```JavaScript title:app.js
const fruits = ["Apple", "Banana", "Orange", "Mango", "Pineapple"];

const lastTwo = fruits.slice(-2);
console.log(lastTwo); // ['Mango', 'Pineapple']
```

In this example, `slice(-2)` extracts the last two elements of the array. When using a negative index with the `slice` method, negative indices are counted from the end of the array, starting at `-1` for the last element, `-2` for the second-to-last element, and so on. The negative index `-2` itself is included because it is the starting point of the extraction.

#### Using a positive start index and a negative end index
```JavaScript title:app.js
const fruits = ["Apple", "Banana", "Orange", "Mango", "Pineapple"];

// Using positive start index and negative end index
const sliceExample = fruits.slice(1, -1);
console.log(sliceExample); // ['Banana', 'Orange', 'Mango']
```

In this example, `slice(1, -1)` starts extracting from index `1` and goes up to, but does not include, the element at index `-1` (which is the last element). This results in a new array with `['Banana', 'Orange', 'Mango']`. The `slice` method always excludes the element at the final index specified, regardless of whether it is positive or negative.

#### Using slice with arrays of objects
In the following example, `slice` creates a new array, `newCar`, from `myCar`. Both include a reference to the object `myHonda`. When the color of `myHonda` is changed to purple, both arrays reflect the change.

```JavaScript title:app.js
// Using slice, create newCar from myCar.
const myHonda = {
  color: "red",
  wheels: 4,
  engine: { cylinders: 4, size: 2.2 },
};
const myCar = [myHonda, 2, "cherry condition", "purchased 1997"];
const newCar = myCar.slice(0, 2);

console.log("myCar =", myCar);
console.log("newCar =", newCar);
console.log("myCar[0].color =", myCar[0].color);
console.log("newCar[0].color =", newCar[0].color);

// Change the color of myHonda.
myHonda.color = "purple";
console.log("The new color of my Honda is", myHonda.color);

console.log("myCar[0].color =", myCar[0].color);
console.log("newCar[0].color =", newCar[0].color);
```

This script writes:

```JavaScript title:app.js
myCar = [
  { color: 'red', wheels: 4, engine: { cylinders: 4, size: 2.2 } },
  2,
  'cherry condition',
  'purchased 1997'
]
newCar = [ { color: 'red', wheels: 4, engine: { cylinders: 4, size: 2.2 } }, 2 ]
myCar[0].color = red
newCar[0].color = red
The new color of my Honda is purple
myCar[0].color = purple
newCar[0].color = purple
```

#### Calling slice() on non-array objects
The `slice()` method reads the `length` property of `this`. It then reads the integer-keyed properties from `start` to `end` and defines them on a newly created array.

```JavaScript title:app.js
const arrayLike = {
  length: 3,
  0: 2,
  1: 3,
  2: 4,
  3: 33, // ignored by slice() since length is 3
};
console.log(Array.prototype.slice.call(arrayLike, 1, 3));
// [ 3, 4 ]
```

#### Using slice() to convert array-like objects to arrays
The `slice()` method is often used with [[js_Function.prototype.bind()|bind()]] and [[js_Function.prototype.call()|call()]] to create a utility method that converts an array-like object into an array.

```JavaScript title:app.js
// slice() is called with `this` passed as the first argument
const slice = Function.prototype.call.bind(Array.prototype.slice);

function list() {
  return slice(arguments);
}

const list1 = list(1, 2, 3); // [1, 2, 3]
```

#### Using slice() on sparse arrays
The array returned from `slice()` may be sparse if the source is sparse.

```JavaScript title:app.js
console.log([1, 2, , 4, 5].slice(1, 4)); // [2, empty, 4]
```