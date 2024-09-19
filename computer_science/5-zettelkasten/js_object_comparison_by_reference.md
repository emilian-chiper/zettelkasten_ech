### Meta
2024-09-19 18:32
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_object_references_and_copying]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let a = {};
let b = a; // copy the reference

console.log( a == b); // true
console.log( a === b); // true

```

### What it does
- Compares two objects by reference.

### How it does it
- In the example above, `a` and `b` reference the same object, thus being equal.
- Here are two independent objects, which look alike, but are not equal.

```JavaScript title:app.js
let a = {};
let b = {};

alert ( a == b ); // false
```

- For comparisons like `obj1 > obj2` or for comparisons against a primitive `obj === 5`, objects are converted to primitives.

#### Const objects can be modified
- An important side effect of storing objects as references is that an object declared as `const` *can* be modified. For instance.

```JavaScript title:app.js
const user = {
	name: 'Jon',
};

user.name = 'Pete';

console.log(user.name); // Pete
```

- It  might seem like line `5` would cause an error, but it does not.
- The value of `user` is constant, in that it references the same object, but the properties of that object are changeable.
- `const user` would give an error only if we were to try to set `user=...` as a whole.