### Meta
2024-10-23 12:02
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_json_methods]]
**State:** #completed 

### JSON methods, toJSoN
Let’s say we have a complex object, and we’d like to convert it into a string in order to send it over a network, or just to output it for logging purposes.

Naturally, such a string should include all important properties.

We could implement the conversion like this:

```JavaScript title:app.js
let user = {
	name: "John",
	age: 30,

	toString() {
		return `{name: "${this.name}", age: ${this.age}}`;
	}
};

alert(user); // {name: "John", age: 30}
```

…But during development, new properties are added, old properties are renamed and removed. Updating `toString` each time can become tedious. We could try to loop over properties in it, but what if the object is complex and has nested objects as properties? We must implement their conversion as well.

This task has been solved already.