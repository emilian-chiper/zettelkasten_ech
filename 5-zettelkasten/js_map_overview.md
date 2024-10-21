### Meta
2024-10-20 23:00
**Tags:** [[javascript_data_types_deep_dive]] [[javascript_map_and_set]] [[js_map]]
**State:** #completed 

Map is a collection of keyed data items, just like `Object`. The main difference is that `Map` allows keys of any type.

Methods and properties are:
- `new Map()` – creates the map.
- `map.set(key, value)` – stores the value by the key.
- `map.get(key)` – returns the value by the key, `undefined` if `key` doesn’t exist in map.
- `map.has(key)` – returns `true` if the `key` exists, `false` otherwise.
- `map.delete(key)` – removes the element (the key/value pair) by the key.
- `map.clear()` – removes everything from the map.
- `map.size` – returns the current element count.

For instance:

```JavaScript title:app.js
let map = new Map();

map.set('1', 'str1'); // a string key
map.set(1, 'num1'); // a numeric key
map.set(true, 'bool1'); // a boolean key

// Map keeps the type, so these two are different:
alert( map.get(1) ); // 'num1'
alert( map.get('1') ); // 'str1'

alert( map.size ); // 3
```

Unlike objects, keys are not converted to strings. Any type of key is possible.

**ℹ️ `map[key]` isn’t the right way to use a `Map`**
Although `map[key]` also works, e.g. we can set `map[key] = 2`, this is treating `map` as a plain JavaScript object, so it implies all corresponding limitations (only string/symbol keys and so on). We should use `set` and `get` methods instead.

**Map can also use objects as keys**
For instance:

```JavaScript title:app.js
let john = { name: "John" };

// for every user, let's store their visits count
let visitCountMap = new Map();

// john is the key for the map
visitsCountMap.set(john, 123);

alert( visitsCountMap.get(john) ); // 123
```

Using objects as keys is one of the most notable and important `Map` features. The same does not count for `Object`.

Let’s try:

```JavaScript title:app.js
let john = { name: "John" };
let ben = { name: "Ben" };

let visitsCountObj = {}; // try to use an object

visitsCountObj[ben] = 234;
visitsCountObj[john] = 123;

alert( visitsCountObj["[object Object]"] ); // 123
```

As `visitsCountObj` is an object, it converts all `Object` keys, such as `john` and `ben` above, to the same string `"[object Object]"`. Not what we want.

**ℹ️ How `Map` compares keys**
To test keys for equivalence, `Map` uses the algorithm [SameValueZero](https://tc39.es/ecma262/#sec-samevaluezero). It is roughly the same as strict equality `===`, but the difference is that `NaN` is considered equal to `NaN`. So `NaN` can be used as the key as well. This algorithm can’t be changed or customized.

**ℹ️ Chaining**
Every `map.set` call returns the map itself, so we can “chain” the calls:
```JavaScript title:app.js
map.set('1', 'str1')
	.set(1, 'num1')
	.set(true, 'bool1')
```