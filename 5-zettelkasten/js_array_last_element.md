### Meta
2024-10-14 11:03
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let fruits = ["apple", "orange", "plum"];

alert (fruits[fruits.length-1]); // plum
```

### What it does
Gets the last element in an array.

### How it does it
Some programming languages allow the use of negative indexed for the same purpose, like `fruits[-1]`. In JavaScript, it won’t work. The result will be `undefined`, because the index in the square brackets is treated literally.

There is a shorter syntax:

```JavaScript title:app.js
let fruits = ["apple", "orange", "plum"];

// same as fruits[fruits.length-1]
alert( fruits.at(-1) ); 
```

In other words, `arr.at(i)`:
- is exactly the same as `arr[i]` for `i >= 0`.
- for negative values of `i`, it steps back from the end of the array.