### Meta
2024-09-30 10:32
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[js_strings_search_substrings]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let str = 'Widget with id';

alert( str.indexOf('Widget') ); // 0
alert( str.indexOf('widget') ); // -1

alert( str.indexOf("id") ); // 1
```

### What it does
- `str.indexOf(substr, pos)`.
- It looks for the `subtst` in `str`, starting with the given position  `pos`, and returns the position (index) where the math was first encountered or `-1` if nothing can be found.
- The optional second parameter allows us to start searching from a given position.

### Use cases
```JavaScript title:app.js
let str = "Widget with id";

alert( str.indexOf('id', 2) ); // 12
```

- If we’re interested in all occurrences, we can run `indexOf` in a loop. Every new call is made with the position after the previous match.

```JavaScript title:app.js
let str = 'As sly as a fox, as strong as an ox';

let target = 'as';'

let position = 0;
while (true) {
	let foundPos = str.indexOf(target, pos);
	if (foundPos == -1) break;

	alert( `Found at ${foundPos}` );
	pos = foundPos + 1; // continue the search from the next position
}
```

- In shorter form:

```JavaScript title:app.js
let str = "As sly as a fo, as strong as an ox";
let target = "as";

let pos = -1;
while ((pos = str.indexOf(target, pos + 1)) != -1) {
	alert( pos );
}
```

#### Variations
- There’s a similar method, `str.lastIndexOf(substr, pos)` that searches from the end of the string to its beginning.
- It lists the occurrences in reverse order.

#### Inconveniences
- There’s a slight inconvenience with `indexOf` in the `if` test. We can’t put the `if` like this:

```JavaScript title:app.js
let str = "Widget with id";

if (str.indexOf("Widget")) {
	alert("We found it"); // doesn't work
}
```

- The `alert` here doesn’t show because `str.indexOf("Widget")` returns `0`, and `if` considers `0` as `false`.
- Thus, we check for `-1`:

```JavaScript title:app.js
let str = "Widget with id";

if (str.indexOf("Widget") != -1) {
	alert("We found it");
}
```