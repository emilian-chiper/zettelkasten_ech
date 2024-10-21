### Meta
2024-10-20 22:31
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_iterables]]
**State:** #completed 

Arrays and strings are most widely used built-in iterables.

For a string, `for..of` loops over its characters:

```JavaScript title:app.js
for (let char of "test") {
	// triggers 4 times: once for each character
	alert( char ); // t, then e, then s, then t
}
```