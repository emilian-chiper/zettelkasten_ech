### Meta
2024-09-30 10:15
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_strings]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
alert( `My\n`.length ); // 3
```

### What it does
- Shows the length of the string.

#### `length` is a property
- **DO NOT** spell `str.length()`.
- `str.length` is a **numeric property**, not a function.