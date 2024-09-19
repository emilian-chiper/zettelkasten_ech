### Meta
2024-09-19 17:20
**Tags:** [[javascript]] [[javascript_object_basics]] [[javavscript_objects_101]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let obj = {
	for: 1,
	let: 2,
	return: 3,
}

console.log( obj.for + obj.let + obj.return ); // 6

```

### What it does
- Object property names bear **NO RESTRICTIONS** in regards to JavaScript's **reserved keywords**.

### How it does it
- There are no limitations on property names.
- They can be any strings or symbols.
- This happens because **other types are automatically converted to strings**.
- For instance, `0` becomes `"0"` when used as a property key.

```JavaScript title:app.js
let objs = {
	0: "test",
};

// both alerts access the same property
alert( obj["0"] ); // test
alert( obj[0] ); // test
```

- There's a minor gotcha with a special property named `__proto__`. We can't set it to a non-object value.

```JavaScript title:app.js
let obj = {}
obj.__proto__ = 5; // assign a number
alert(obj.__proto__); // [object Object] - the value is an object, didn't work as intended
```
