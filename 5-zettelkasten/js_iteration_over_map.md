### Meta
2024-10-20 23:20
**Tags:** [[javascript_data_types_deep_dive]] [[javascript_map_and_set]] [[js_map]]
**State:** #completed 

For looping over a `map`, there are 3 methods:
- `map.keys()` – returns an iterable for keys,
- `map.values()` – returns an iterable for values,
- `map.entries()` – returns an iterable for entries `[key, value]`, it’s used by default in `for..of`.

For instance:
```JavaScript title:app.js
let recipeMap = new Map([
	['cucumber', 500],
	['tomatoes', 350],
	['onion', 50]
]);

// iterate over keys (vegetables)
for (let vegetable of recipeMap.kesy()) {
	alert(vegetable); // cucumber, tomatoes, onion
}

// iterate over values (amounts)
for (let amount of recipeMap.values()) {
	alert(amount); // 500, 350, 50
}

// iterate over [key, value] entries
for (let entry of recipeMap) { // the same as recipeMap.entries
	alert(entry); // cucumber, 500 (and so on)
}
```

**ℹ️ The insertion order is used**
The iteration goes in the same order as the values were inserted. `Map` preserves this order, unlike a regular `Object`.

Besides that, `Map` has a built-in `forEach` method, similar to `Array`:
```JavaScript title:app.js
// runs the function foreach (key, value) pair
recipeMap.forEach( (value, key, map) => {
	alert(`${key}: ${value}`); // cucumber: 500 etc
});
```