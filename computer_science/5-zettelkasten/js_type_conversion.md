### Meta
2024-09-17 22:50
**Tags:** [[javascript]] [[javascript_fundamentals]]
**State:** #completed  

### String Conversion
```JavaScript title:app.js
let value = true;
console.log(typeof value); // boolean

value = String(value); // 'true'
console.log(typeof value); // string
```

### Number conversion
```JavaScript title:app.js
let str = "123";
console.log(typeof str); // string

let num = Number(str) // 123
console.log(typeof num); // number
```

#### Number conversion rules
- `undefined` becomes `NaN`
- `null` becomes `0`
- `true` and `false` become `1` and `0`
- `string`
	- Whitespaces (including spaces, tabs `\t`, newlines `\n` etc.) from the start and end are removed.
	- If the remaining string is empty, the result is `0`. Otherwise, the number is "read" from the string.
	- An error gives `NaN`.

### Boolean Conversion
```JavaScript title:app.js
console.log( Boolean(1) ); // true
console.log( Boolean(0) ); // false

console.log( Boolean("hello") ); // true
console.log( Boolean("") ); // false
```

#### Conversion rules
- Values that are intuitively "empty", like the number `0`, an empty string `''`, `null`, `undefined`, and `NaN` become `false`.
- Other values become `true`.
- **Note:** unlike other languages (namely [[PHP]]), `"0"` is regarded as a `truthy` value, since it is a non-empty string, thus returning `true` when converted to Boolean.