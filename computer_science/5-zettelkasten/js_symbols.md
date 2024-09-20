### Meta
2024-09-20 11:27
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_symbol_type]]
**State:** #completed  ``

### What it looks like
```JavaScript title:app.js
let id = Symbol();

```

### What it does
- A symbol represents a unique identifier.

### How it does it
- Upon creation, we can give symbols a description (also called symbol name), mostly useful for debugging purposes:

```JavaScript title:app.js
// id is a symbold with the description "id"
let id = Symbol("id");
```

- Symbols are guaranteed to be unique.
- Even if we create many symbols with the exact same description, they are different values.
- The description is just a label, with no other effect.

```JavaScript title:app.js
let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```

#### Symbols do NOT auto-convert to a string
- Most values in JavaScript support implicit conversion to a string.
- Symbols do not.

```JavaScript title:app.js
let id = Symbol("id");
alert(id); // TypeError: Cannot convert a Symbol value to a string
```

- That's a "language guard".
- If we really want to show a symbol, we need to explicitly call `.toString()` on it.
```JavaScript title:app.js
let id = Symbol("id");
alert(id.toString()); // Symbol(id)
```

- `symbol.description` show only the description.

```JavaScript title:app.js
let id = Symbol("id");
alert(id.description); // id
```