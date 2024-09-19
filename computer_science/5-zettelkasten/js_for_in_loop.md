### Meta
2024-09-19 17:54
**Tags:** [[javascript]] [[javascript_object_basics]] [[javavscript_objects_101]]
**State:** #pending 

### What it looks like
```JavaScript title:app.js
for (key in object) {
	// ...
}
```

### What it does
- Iterates over all keys of an object.

### How it does it
- Let's output all properties of `user`:

```JavaScript title:app.js
let user = {
	name: 'Jon',
	age: 30,
	isAdmin: true,
}

for (let key in user) {
	// keys
	alert( key ); // name, age, isAdmin
	// values for the keys
	alert( user[key] ); // Jon, 
}
```
