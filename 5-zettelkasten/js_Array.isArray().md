### Meta
2024-10-20 21:39
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_array_methods]]
**State:** #completed 

Arrays do not form a separate language type. They are based on objects.

To `typeof` doesn’t help to distinguish a plain object from an array:

```JavaScript title:app.js
alert(typeof {}); // object
alert(typeof []); // object
```

… But arrays are used so often that there’s a special method for that. `Array.isArray(value)` returns `true` if the `value` is an array, and `false` otherwise.

```JavaScript title:app.js
alert(Array.isArray({})); // false
alert(Array.isArray([])); // true
```