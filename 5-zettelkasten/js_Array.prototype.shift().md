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
#### Removing an element from an array
The following code displays the `myFish` array before and after removing its first element. It also displays the removed element:

```JavaScript title:app.js
const myFish = ["angel", "clown", "mandarin", "surgeon"];

console.log("myFish before:", myFish);
// myFish before: ['angel', 'clown', 'mandarin', 'surgeon']

const shifted = myFish.shift();

console.log("myFish after:", myFish);
// myFish after: ['clown', 'mandarin', 'surgeon']

console.log("Removed this element:", shifted);
// Removed this element: angel
```

#### Using shift() method in while loop
The `shift()` method is often used in condition inside while loop. In the following example, every iteration will remove the next element from an array, until it’s empty:

```JavaScript title:app.js
const names = ["Andrew", "Tyrone", "Paul", "Maria", "Gayatri"];

while (typeof (i = names.shift()) !== "undefined") {
  console.log(i);
}
// Andrew, Tyrone, Paul, Maria, Gayatri
```

#### Calling shift() on non-array objects
The `shift()` method reads the `length` property of `this`. If the normalized length is 0, `length` is set to `0` again (whereas it may be negative or `undefined` before). Otherwise, the property at `0` is returned, and the rest of the properties are shifted left by one. The `length` property is decremented by one.

```JavaScript title:app.js
const arrayLike = {
  length: 3,
  unrelated: "foo",
  2: 4,
};
console.log(Array.prototype.shift.call(arrayLike));
// undefined, because it is an empty slot
console.log(arrayLike);
// { '1': 4, length: 2, unrelated: 'foo' }

const plainObj = {};
// There's no length property, so the length is 0
Array.prototype.shift.call(plainObj);
console.log(plainObj);
// { length: 0 }
```