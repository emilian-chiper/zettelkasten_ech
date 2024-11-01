### Meta
2024-10-23 12:07
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_json_methods]]
**State:** #completed 

### JSON.stringify
The JavaScript Object Notation (JSON) is a general format to represent values and objects.

JavaScript provides the following methods:
- `JSON.stringify` to convert objects into JSON.
- `JSON.parse` to convert JSON back into an object.

For example, here we `JSON.stringify` a student:

```JavaScript title:app.js
lest student = {
	name: 'John',
	age: 30,
	isAdmin: false,
	courses: ['html', 'css', 'js'],
	spouse: null,
};

let json = JSON.stringify(student);

alert(typeof json); // String

alert(JSON);
/* JSON-encoded object:
{
  "name": "John",
  "age": 30,
  "isAdmin": false,
  "courses": ["html", "css", "js"],
  "spouse": null
}
*/
```

The resulting string is called a *JSON-encoded* or *serialized* or *stringified* or *marshalled* object, ready to be sent over the wire or put into a plain data store.

Note that JSON-encoded objects have several important differences from object literals:
- Strings use double quotes. No single quotes or backticks in JSON. So `'John'` becomes `"John"`.
- Object property names are double-quoted also. That’s obligatory. So `age: 30` becomes `"age": 30`.

`JSON.stringify` can be also applied to primitives.

JSON supports the following data types:
- Objects `{...}`
- Arrays `[...]`
- Primitives:
	- strings,
	- numbers,
	- boolean values,
	- `null`.

```JavaScript title:app.js
// a number in JSON is just a number
alert( JSON.stringify(1) ); // 1

// a string in JSON is still a string, but double-quoted
alert( JSON.stringify('test') ); // "test"

alert( JSON.stringify(true) ); // true

alert( JSON.stringify([1, 2, 3]) ); // [1, 2, 3]
```

JSON is data-only language-independent specification, so some JavaScript specific object properties are skipped by `JSON.stringify`. Namely:
- Function properties (methods),
- Symbolic keys and values,
- Properties that store `undefined`.

```JavaScript title:app.js
let user = {
	sayHi() { // ignored
		alert("Hello");
	},
	[Symbol("id")]: 123, // ignored
	something: undefined, // ignored
}

alert( JSON.stringify(user) ); // {} (empty object)
```

If that’s not what we need, we can customize the process.

Nested objects are supported and converted automatically. For instance:

```JavaScript title:app.js
let meetup = {
	title: "Conference",
	room: {
		number: 23,
		participants: ["john", "ann"],
	}
};

alert( JSON.stringify(meetup) );
/* The whole structure is stringified:
{
  "title":"Conference",
  "room":{"number":23,"participants":["john","ann"]},
}
*/
```

**Limitation:** there must be *no* circular references. For instance:

```JavaScript title:app.js
let room = {
	number: 23,
};

let meetup = {
	title: "Conference",
	participants: ["john", "ann"]
};

meetup.place = room;
room.occupiedBy = meetup;

JSON.stringify(meetup); // Error
```

The conversion fails because of the circular reference: `room.occupiedBy` references `meetup`, and `meetup.place` references `room`.