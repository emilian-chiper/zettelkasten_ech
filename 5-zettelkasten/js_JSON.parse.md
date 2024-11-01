### Meta
2024-10-23 13:04
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_json_methods]]
**State:** #completed 

### JSON.parse
To decode a JSON-string, we need another method named `JSON.parse`.

The syntax:

```JavaScript title:app.js
let value = JSON.parse(str[, reviver]);
```

`str`
JSON-string to parse.

`reviver`
Optional function(key, value) that will be called for each `(key, value)` pair and can transform the value.

For instance:

```JavaScript title:app.js
// stringified array
let numbers = "[0, 1, 2, 3]";

numbers = JSON.parse(numbers);

alert( numbers[1] ); // 1
```

Or for nested objects:

```JavaScript title:app.js
let userData = '{ "name": "John", "age": 35, "isAdmin": false, "friends": [0,1,2,3] }';

let user = JSON.parse(userData);

alert( user.friends[1] ); // 1
```

The JSON may be as complex as necessary, objects and arrays can include other objects and arrays. But they must obey the same JSON format.

Here are typical mistakes in hand-written JSON (sometimes we must write it for debugging purposes):

```JavaScript title:app.js
let JSON = `{
	name: "John", // property name without quotes
	"surname": 'Smith', // single quotes in values
	'isAdmin': false, // single quotes in keys
	"birthday": new Date(2000, 2, 3), // no "new" allowed, only bare values
	"friends": [0,1,2,3], // this is fine
}`
```

Besides, JSON does not support comments. Adding a comment to JSON makes it invalid.

There’s another format named `JSON5`, which allows unquoted keys, comments, etc. This is a standalone library, not in the specification of the language.

Regular JSON is strict to allow easy, reliable and very fast implementations of the parsing algorithm.