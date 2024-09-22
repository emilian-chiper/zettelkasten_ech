### Meta
2024-09-20 21:09
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_numbers]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let num = 255;

alert( num.toString(16) ); // ff
alert( num.toString(2) ); // 11111111
```

### What it does
- Returns a string representation of `num` in the numeral system with the given `base`.

### How it does it
- The base can vary from `2` to `36`. By default, it's `10`.

#### Use cases
- **base=16** is used for hex colors, character encodings, etc. Digits can be `0 ... 9` or `A ... F`.
- **base=2** is mostly for debugging bitwise operations. Digits can be `0` or `1`.
- **base=36** is the maximum. Digits can be `0 ... 9` or `A ... Z`. The whole Latin alphabet is used to represent a number. A use case is when we need to turn a long numeric identifier into something shorter, for example, to make a short url. Can simply represent it in the numeral system with base `36`:

```JavaScript title:app.js
alert( 123456..toString(36) ); // 2n9c
```

#### Two dots to call a method
- The above instance `123456..toString(36)` is not a typo.
- If we want to call a method directly on a number, like `toString` in the example above, then we need to place two dots `..` after it.
- If we placed a single dot: `123456..toString(36)`, then there would be an error, because JavaScript syntax implies the decimal part after the first dot.
- Alternately, we could write `(123456).toString(36)`.