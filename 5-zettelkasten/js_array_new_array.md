### Meta
2024-10-14 13:14
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let arr = new Array('apple', 'pear', 'etc');
```

### What it does
Creates an instance of the `Array` class.

### How it does it
This syntax is rarely used, because square brackets `[]` are shorter. Also, there’s a tricky feature with it.

If `new Array` is called with a single argument which is a number, then it creates an array *without items, but with the given length*.

```JavaScript title:app.js
let arr = new Array(2); // wil create an array of length 2

alert( arr[0] ); // undefined

alert( arr.length ); // 2
```

To avoid such surprises, we use square brackets.