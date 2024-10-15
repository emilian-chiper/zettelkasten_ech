### Meta
2024-10-14 13:01
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let arr = ['apple', 'orange', 'pear'];

// for loop
for (let i = 0; i < arr.length; i++) {
	alert( arr[i] );
}

// for..of
for (let fruit of fruits) {
	alert(fruit);
}

// for..in
for (let key in arr) {
	alert(arr[key]);
}
```

### What it does
The `for` and `for..of` loops work as expected.

### Complications
Technically, because arrays are objects, it’s also possible to use `for..in`.

However, that’s a bad idea. Potential problems:
1. The `for..in` loop operates over *all properties*, not only the numeric ones.
	There are so-called ‘array-like’ objects in the browser and in other environments, that *look like arrays*. That is, they have `lenght` and `index` properties, but they may also have other non-numeric properties and methods, which we usually don’t need. The `for..in` loop will list them too. So if we need to work with array-like objects, these extra properties and methods can become a pain.
2. The `for..in` loop is optimized for generic objects, not arrays, and thus 10-100 times slower. Of course, it’s still very fast. The speedup may only matter in bottlenecks. But still we should be aware of the difference.

Generally, we shouldn’t use `for..in` for arrays.
