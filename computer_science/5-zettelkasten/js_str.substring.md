### Meta
2024-09-30 11:13
**Tags:** [[javascript_data_types_deep_dive]] [[javascript_strings]] [[js_strings_get_substrings]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let str = "stringify";

// these are same for substring
alert( str.substring(2, 6) ); // "ring"
alert( str.substring(6, 2) ); // "ring"

// ... but not for slice
alert( str.slice(2, 6) ); // "ring"
alert( str.slice(6, 2) ); // ""
```

### Format
`str.substring(start, [, end])`

### What it does
- Returns the part of the string *between* `start` and `end` (not including `end`).
- This is almost the same as `slice`, but allows `start` to be greater than `end`.
- Negative arguments are **NOT SUPPORTED**. They are treated as `0`.