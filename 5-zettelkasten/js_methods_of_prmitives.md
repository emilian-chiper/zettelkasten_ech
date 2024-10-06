### Meta
2024-09-20 17:23
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_methods_of_primitives]]
**State:** #completed  

### Primitives vs. Objects
- A **primitive**:
	- Is a value of a primitive type.
	- There are 7 primitive types: `string`, `number`, `bigInt`, `boolean`, `symbol`, `null` and `undefined`.
- An **object**:
	- Is capable of storing multiple values as properties.
	- Can be created with `{}`. There are other kinds of objects in JavaScript.
- An object can store a function as one of its properties

```JavaScript title:app.js
let jon = {
	name: 'Jon',
	sayHi: function() {
		alert("Hi buddy!");
	}
};

john.sayHi(); // Hi buddy!
```

- Many built-in objects already exist, such as those that work with dates, errors, HTML elements, etc. They have different properties and methods.
- But these features come with a cost.
- Objects are 'heavier' than primitives -- they require additional resources.