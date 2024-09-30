### Meta
2024-09-30 10:19
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_strings]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let str = `Hello`;

alert( str[0] ); // H
alert( str.at(0) ); // H

alert( str[str.length - 1] ); // o
alert( str.at(-1) ); // 0
```

### What happens
- Both the square brackets `[pos]` and the method call `str.at(pos)` return the character at the specified position (index).
- If `pos` is negative, it’s counted from the end of the string.

### Particularities
- The square brackets always return `undefined` for negative indexes:

```JavaScript title:app.js
let str = `Hello`;

alert( str[-2] ); // undefined
alert( str.at(-2) ); // l
```

- We can also iterate over characters using `for ... of`:

```JavaScript title:app.js
for (let char of "Hello") {
	alert(char); // H,e,l,l,o
}
```