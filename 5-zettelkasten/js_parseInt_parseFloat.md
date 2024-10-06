### Meta
2024-09-29 21:48
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_numbers]]
**State:** #completed 

### The problem
```JavaScript title:app.js
alert(+"100px"); // NaN
```

### What happens
- Numeric conversion using a plus `+` or `Number()` is strict. If a value is not exactly a number, it fails.
- The sole exception is trailing spaces, which are ignored.

### Solution
```JavaScript title:app.js
alert( parseInte('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5

alert( parseInt('12.3') ); // 12
alert( parseFloat('12.3.4') ); // 12.3, second point stops the reading
```

- Sometimes we encounter `NaN`.
```JavaScript title:app.js
alert( pareseInt('a123') ); // NaN, the first symbol stops the process
```

#### The second argument
- `parseInt` has an optional second parameter.
- It specifies the base of the numeral system, so `parseInt` can also parse strings of hex numbers, binary, numbers, etc.

```JavaScript title:app.js
alert( parseInt('0xff', 16) ); // 255
alert( parseInt('ff', 16) ); // 255, without 0x also works

alert( parseInt('2n9c', 36) ); // 123456
```