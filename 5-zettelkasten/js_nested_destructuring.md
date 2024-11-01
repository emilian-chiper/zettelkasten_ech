### Meta
2024-10-22 21:00
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_destructuring_assignment]]
**State:** #completed 

### Nested destructuring
If an object or an array contains other nested objects and arrays, we can use more complex left-side patterns to extract deeper portions.

In the code below `options` has another object in the property `size` and an array in the property `items`. The pattern on the left side of the assignment has the same structure to extract values from them:

```JavaScript title:app.js
let options = {
	size: {
		width: 100,
		height: 200,
	},
	items: ["Cake", "Doghnut"],
	extra: true,
};

// destructuring assignment split in multiple lines for clarity
let {
	size: {
		width,
		height,
	},
	items: [item1, item2], // assign items here
	title = "Menu" // not present in the object (using default value)
} = options;

alert(title); // Menu
alert(width);  // 100
alert(height); // 200
alert(item1);  // Cake
alert(item2);  // Doughnut
```

All properties of `options` except `extra`, which is absent in the left part, are assigned to corresponding variables.

Note that there are no variables for `size` and `items`, as we take their contents instead.