### Meta
2024-10-20 23:26
**Tags:** [[javascript_data_types_deep_dive]] [[javascript_map_and_set]] [[js_map]]
**State:** #pending 

### Object.entries: Map from Object
When a `Map` is created, we can pass an array (or another iterable) with key/value pairs for initialization, like this:
```JavaScript title:app.js
// array of [key, value] pairs
let map = new Map([
	['1', 'str1'],
	[1, 'num1'],
	[true, 'boot1']
]);

alert( map.get('1') ); // str1
```

If we have a plain object, and we’d like to create a `Map` from it, then we can use built-in method `Object.entrie(obj)` that returns an array of key/value pairs for an object exactly in that form.

So we can create a map from an object like this:
```JavaScript title:app.js
let obj = {
	name: "John",
	age: 30
};

let map = new Map(Object.entries(obj));

alert( map.get('name') ); // John
```

Here, `Object.entries` returns the array of key/value pairs: `[ ["name", "John"], ["age", 30] ]`. That’s what `Map` needs.