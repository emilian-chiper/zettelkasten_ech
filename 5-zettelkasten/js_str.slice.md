### Meta
2024-09-30 11:09
**Tags:** [[javascript_data_types_deep_dive]] [[javascript_strings]] [[js_strings_search_substrings]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let str = "stringify";
alert( str.slice(0, 5) ); // 'strin'
alert( str.slice(0, 1) ); // 's'
```

### Formatting
`str.slice(star [, end]`

### What it does
- Returns the part of the string from `start` to (but not including) `end`.
- If there is no second argument, then `slice` goes till the end of the string.