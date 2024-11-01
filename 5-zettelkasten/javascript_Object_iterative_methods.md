### Meta
2024-10-22 12:02
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]]
**State:** #completed 

### Object.keys, values, entries
For plain objects, the following methods are available:
- [Object.keys(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) – returns an array of keys.
- [Object.values(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values) – returns an array of values.
- [Object.entries(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) – returns an array of `[key, value]` pairs.

Compared to `map.keys()`, the object variant `Object.keys(obj)` does *not* return an iterable, but an actual *array*.

 The first difference between maps and objects is that we must call `Object.keys(obj)`, and not `obj.keys`. The main reason is flexibility.

Objects area  base for all complex structures in JavaScript. So we may have an object of our own (e.g. `data`) that implements its own `data.values()` method. And we can still call `Object.values(data)` on it.

The second difference is that `Object.*` methods return “real” array objects, not just an iterable. That’s mainly for historical reasons.

For example:

```JavaScript title:app.js
let user = {
	name: "John",
	age: 30,
}
```

- `Object.keys(user) = ["name", "age"]`
- `Object.values(user) = ["John", 30]`
- `Object.entries(user) = [ ["name", "John"], ["age", 30] ]`

Here’s an example using `Object.values` to loop over property values:

```JavaScript title:app.js
let user = {
	name: "John",
	age: 30,
};

// loop over values
for (let value of Object.values(user)) {
	alert(value); // John, then 30
}
```

**⚠️ Object iterable methods ignore symbolic properties**
Just like a `for..in` loop, these methods ignore properties that use `Symbol(...)` as keys.

Usually, that’s convenient, but if we want symbolic keys too, then there’s a separate method `Object.getOwnPropertySymbols` that returns an array of only symbolic keys. Also, there’s a method `Reflect.ownKeys(obj)` that returns *all* keys.

### Transforming objects
Objects lack many methods that exist for arrays, e.g. `map`, `filter`, etc.

If we’d like to apply them, we can use `Object.entries` followed by `Object.fromEntries`:
1. Use `Object.entries(obj)` to get an array of key/value pairs from `obj`.
2. Use array methods on that array, e.g. `map`, to transform these key/value pairs.
3. Use `Object.fromEntries(array)` on the resulting array to turn it back into an object.

For example, we have an object with prices, and would like to double them:

```JavaScript title:app.js
let prices = {
	banana: 1,
	orange: 2,
	meat: 4,
}

let doublePrices = Object.fromEntries(
	Object.entries(prices).map(entry => [entry[0], entry[1] * 2])
)

alert(doublePrices.meat); // 8
```