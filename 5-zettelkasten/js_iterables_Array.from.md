### Meta
2024-10-20 22:44
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_iterables]]
**State:** #completed 

There’s a universal method `Array.from` that takes an iterable or array-like value and makes a ‘real’ `Array` from it. Then we can call array methods on it.

For instance:

```JavaScript title:app.js
let arrayLike = {
	0: "Hello",
	1: "World",
	length: 2
};

let arr = Array.from(arrayLike); // (*)
alert(arr.pop()); // World (method works)
```

`Array.from` at the line `(*)` takes the object, examines it for being an iterable or array-like, then makes a new array and copies all items to it.

The same happens for an iterable:

```JavaScript title:app.js
// assuming that range is taken from the example above
let arr = Array.from(range);
alert(arr); // 1,2,3,4,5 (array toString conversion works)
```

The full syntax for `Array.from` also allows us to provide an optional “mapping” function:

```JavaScript title:app.js
Array.from(obj[, mapFn, thisArg])
```

The optional second argument `mapFn` can be a function that will be applied to each element before adding it to the array, and `thisArg` allows us to set `this` for it.

For instance:

```JavaScript title:app.js
// assuming that range is taken from the example above

// square each number
let arr = Array.from(range, num => num * num);

alert(arr); // 1,4,9,16,25
```

Here we use `Array.from` to turn a string into an array of characters:

```JavaScript title:app.js
let str = '𝒳😂';

// splits str into array of characters
let chars = Array.from(str);

alert(chars[0]); // 𝒳
alert(chars[1]); // 😂
alert(chars.length); // 2
```

Unlike `str.split`, it relies on the iterable nature of the string and so, just like `for..of`, correctly works with surrogate pairs.

Technically here it does the same as:

```JavaScript title:app.js
let str = '𝒳😂';

let chars = []; // Array.from internally does the same loop
for (let char of str) {
  chars.push(char);
}

alert(chars);
```

… But it is shorter.

We can even build surrogate-aware `slice` on it:

```JavaScript title:app.js
function slice(str, start, end) {
  return Array.from(str).slice(start, end).join('');
}

let str = '𝒳😂𩷶';

alert( slice(str, 1, 3) ); // 😂𩷶

// the native method does not support surrogate pairs
alert( str.slice(1, 3) ); // garbage (two pieces from different surrogate pairs)
```