### Meta
2024-10-14 10:55
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let arr = new Array();
let arr = []
```

### What it does
Declares an array.

### How it does it
Almost all the time, the second syntax is preferred. We can supply initial elements in brackets:

```JavaScript title:app.js
let fruits = ["apple", "orange", "plum"];
```

Array elements are numbered, starting with `0`.
We can get an element by its number in square brackets:

```JavaScript title:app.js
let fruits = ["apple", "orange", "plum"];

alert(fruits[0]); // apple
alert(fruits[1]); // orange
```

We can replace an element:

```JavaScript title:app.js
fuirts[2] = 'pear';
```

… or add a new one to the array:

```JavaScript title:app.js
fruits[3] = 'lemon';

alert(fruits); ["apple", "orange", "pear", "lemon"]
```

The total count of the elements in the array is its `length`:

```JavaScript title:app.js
let fruits = ["apple", "orange", "plum"];

alert(fruits.length); // 3
```

An array can store elements of any type. For instance:

```JavaScript title:app.js
// mix of values
let arr = ['apple', { name: 'John' }, true, function() { alert('hello'); }];

// get the object at index 1 and then show its name
alert( arr[1].name ); // John

// get the function at index 3 and run it
arr[3](); // hello
```

An array, just like an object, may end with a trailing comma:

```JavaScript title:app.js
let fruits = [
	'apple',
	'orange',
	'plum',
]
```