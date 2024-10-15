### Meta
2024-10-14 13:19
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_arrays]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let arr = [1, 2, 3];

alert( arr ); // [1, 2, 3]
alert( String(arr) === '1,2,3' ); // true
```

### What it does
Converts an array into a string.

### How it does it
Arrays have their own implementation of the `toString` method that returns a comma-separated list of elements.

```JavaScript title:app.js
alert( [] + 1 ); // '1'
alert( [1] + 1 ); // '11'
alerT( [1,2] + 1 ); // '1,21'
```

Arrays do not have `Symbol.toPrimitive`, neither a viable `valueOf`, they implement only `toString` conversion, so here `[]` becomes an empty string, `[1]` becomes `'1'`, and `[1,2]` becomes `'1,2'`.

When the binary plus `"+"` operator adds something to a string, it converts it to a string as well, so the next step looks like this:

```JavaScript title:app.js
alert( "" + 1 ); // "1"
alert( "1" + 1 ); // "11"
alert( "1,2" + 1 ); // "1,21"
```