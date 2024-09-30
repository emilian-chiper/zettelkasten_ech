### Meta
2024-09-30 10:47
**Tags:** [[javascript_data_types_deep_dive]] [[javascript_strings]] [[js_strings_search_substrings]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
alert( "Widget with id".includes("Widget") ); // true

alert( "Hellow".includes("Bye") ); // false
```

### What it does
- `str.includes(substr, pos)`. 
- Returns `true` or `false` depending on whether `str` contains `substr` within. 
- The optional second argument `pos` is the position to start searching from.