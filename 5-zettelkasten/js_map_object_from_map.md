### Meta
2024-10-20 23:34
**Tags:** [[javascript_data_types_deep_dive]] [[javascript_map_and_set]] [[js_map]]
	**State:** #completed 

### Object.fromEntries: Object from Map
There’s `Object.fromEntries` method that does the reverse: given an array of `[key, value]` pairs, it creates an object from them:
```JavaScript title:app.js
let prices = Object.fromEntries([
	['banana', 1],
	['orange', 2],
	['meat', 4]
]);

// now prices = { banana: 1, orange: 2, meat: 4 }

alert(prices.orange); // 2
```

We can use `Object.fromEntries` to get a plain object from `Map`.

```JavaScript title:app.js
let map = new Map();
map.set('banana', 1);
map.set('orange', 2);
map.set('meat', 4);

let obj = Object.fromEntries(map.entries()); // make a plain object (*)

// done!
// obj = { banana: 1, orange: 2, meat: 4 }

alert(obj.orange); // 2
```

All call to `map.entries()` returns an iterable of key/value pairs, exactly in the right format for `Object.fromEntries`.

We can also make it shorter:

```JavaScript title:app.js
let obj = Object.fromEntries(map); // omit .entries()
```

That’s the same, because `Object.fromEntries` expects an iterable object as the argument. Not necessarily an array. And the standard iteration for `map` returns same key/value pairs as `map.entries()`.