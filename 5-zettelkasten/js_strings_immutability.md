### Meta
2024-09-30 10:24
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_strings]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let str = 'Hi';

str[0] = 'h';
alert( str[0] ); // doesn't work
```

### What happens
- Strings can’t be changed in JavaScript. It is impossible to change a character.

### Workaround
- Create a whole new string and assign it to `str` instead of the old one.

```JavaScript title:app.js
let str = 'Hi';

str = 'h' + str[1]; // replace the string

alert( str ); // hi 
```
