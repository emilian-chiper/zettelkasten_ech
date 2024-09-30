### Meta
2024-09-30 11:19
**Tags:** [[javascript_data_types_deep_dive]] [[javascript_strings]] [[js_strings_get_substrings]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let str = "stringify";
alert( str.substr(2, 4) ); // 'ring'
```

### Format
`str.substr(start [, length])`

### What it does
- Returns a part of the string from `start`, with the given `length`.
- Allows us to specify `length` over ending position.
- The first argument may be negative, to count from the end.
- Only browser-hosted JavaScript engines should support it, and it’s not recommended to use it.