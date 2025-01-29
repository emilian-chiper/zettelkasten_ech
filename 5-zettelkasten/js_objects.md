### Meta
2024-09-19 11:40
**Tags:** [[javascript]] [[javascript_object_basics]] [[javavscript_objects_101]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30
};
```

### What it does
- Stores keyed collections of various data and more complex entities.

### How it does it
- An object can be created with figure brackets `{...}` with an optional list of *properties*.
- A *property* is a `key: value` pair, where:
	- the `key` is a `string`, also called 'property name', and
	- the `value` can be anything.
- An empty object can be created using one of two syntaxes:

```JavaScript title:app.js
// Object constructor
let user = new Object();

// Object literal
let user = {};
```
