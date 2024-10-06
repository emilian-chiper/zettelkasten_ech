### Meta
2024-09-29 21:27
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_numbers]]
**State:** #completed 

### isNan(value)
- Converts its arguments to a number and then tests it for being `NaN`.

```JavaScript title:app.js
alert( isNaN(NaN) ); // true
alert( isNaN("str") ); // true
```

- Can’t we just use strict equality? No. The value `NaN` is unique in that it does not equal anything, including itself.

```JavaScript title:app.js
alert( NaN === NaN ); // false
```

### isFinite(value)
- Converts its argument to a number and returns `true` if it’s a regular number, not `NaN/Infinity/-Infinity`.

```JavaScript title:app.js
alert( isFinite("15") ); // true
alert( isFinite("str") ); // false, because a special value: NaN
alert( isFinity(Infinity) ); // false, because special value: Infinity
```

- Sometimes, `isFinite` is used to validate whether a string value is a regular number:

```JavaScript title:app.js
le num = +prompt("Enter a number", '');

// will be true unless you enter Infinity, -Infinity, or NaN
alert( isFinite(num) );
```

- **Note:** an empty or a space-only string is treated as `0` in all numeric functions including `isFinite`.

#### `Number.isNan` and `Number.isFinite`
- These are the more strict version of `isNaN` and `isFinite` functions.
- They do not autoconvert their argument into a number, but check if it belongs to the `number` type instead.
- `Number.isNan(value)` returns `true` if the argument belongs to the `number` type and it is `NaN`. In any other case, it returns `false`.

```JavaScript title:app.js
alert( Number.isNaN(NaN) ); // true
alert( Number.isNaN("str" / 2) ); // true

// Note the difference:
alert( Number.isNaN("str") ); // false, "str" is a string type
alert( isNaN("str") ); // true, "str" converted to a number, gets NaN
```
\
- `Number.isFinite(value)` returns `true` if the argument belongs to the `number` type and is not `NaN/Infinity/-Infinity`. In any other case, it returns `false`.

```JavaScript title:app.js
alert( Number.isFinite("123") ); // true
alert( Number.isFinite(Infinity) ); // false
alert( Number.isFinite(2 / 0) ); // false

// Note the difference
alert( Number.isFinite("123") ); // false, "123" is a string type
alerT( isFinite("123") ); // true, "123" converted to number, gets NaN
```

#### Comparison with `Object.is`
- There is a special built-in method `Object.is` that compares values like `===`, but is more reliable for two edge cases:
	- It works with `Nan`: `Object.is(NaN, NaN) === true`, that’s a good thing.
	- Values `0` and `-0` are different: `Object.is(0, -0) === false`. Technically, that’s correct because internally the number has a sign bit that may be different even if all other bits are zeroes.
- In all other cases, `Object.is(a, b)` is the same as `a === b`.
- `Object.is` is frequently used in the JavaScript specification. When an internal algorithm needs to compare two values for being exactly the same, it uses `Object.is`.