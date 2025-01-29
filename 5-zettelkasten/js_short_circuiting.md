### Meta
2024-09-20 09:02
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_optional_chaining]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = null'
let x = 0;

user?.sayHi(x++); // no 'user'

alert(x); // 0
```

### What it does
- `?.` immediately "short-circuits" the evaluation if the left part doesn't exist.

### How it does it
- If there are any further function calls or operations to the right of `?.`, they won't be made.
