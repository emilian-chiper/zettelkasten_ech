### Meta
2024-10-14 13:09
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let fruits = [];
fruits[123] = 'apple';

alert( fruits.length ); // 124
```

### What it does
The `length` property shows the length of the array.

### What happens
The `length` property automatically updates when we modify the array. To be precise, it is actually not the count of values in the array, but the greatest numeric index plus one.

For instance, a single element with a large index gives a big length.

Note that we usually don’t use arrays as exemplified above.

Another interesting thing about the `length` property is that it’s writeable.

If we increase it manually, nothing interesting happens. But if we decrease it, the array is truncated. The process is irrreversible.

```JavaScript title:app.js
let arr = [1, 2, 3, 4, 5];

arr.length = 2; // truncate to 2 elements
alert( arr ); // [1, 2]

arr.length = 5; // return lenght back
alert( arr[3] ); // undefined: the values do not return
```

So, the simplest way to clear the array is: `arr.length = 0`.