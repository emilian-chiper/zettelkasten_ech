### Meta
2024-10-22 13:43
**Tags:** [[javascript]] [[javascript_data_types_deep_dive]] [[javascript_destructuring_assignment]]
**State:** #completed 

### What it looks like
```JavaScript title:app.js
let {var1, var2} = {var1:..., var2:...};
```

### What’s going on
We should have an existing object on the right side, that we want to split into variables. The left side contains an object-like “pattern” for corresponding properties. In the simplest case, that’s a list of variable names in `{...}`.

For instance:

```JavaScript title:app.js
let options = {
	title: "Menu",
	width: 100,
	height: 200,
};

let {title, width, height} = options;

alert(title); // Menu
alert(width); // 100
alert(height); // 200
```

Properties `options.title`, `options.width` and `options.height` are assigned to the corresponding variables.

The order doesn’t matter. This also works:

```JavaScript title:app.js
// changed the order on the left side {...}
let {height, width, title} = { title: "Menu", height: 200, width: 100 }
```

The pattern on the left side may be more complex and specify the mapping between properties and variables.

If we want to assign a property to a variable with another name, for instance make `options.width` go into the variable named `w`, then we can set the variable name using a colon:

```JavaScript title:app.js
let options = {
	title: "Menu",
	width: 100,
	height: 200,
};

// { srouceProperty: targetVariable }
let{ widht: w, height: h, title } = options;
```

The colon shows “what: goes where”.

For potentially missing properties, we can assign default values with `=`, like this:

```JavaScript title:app.js
let options = {
	title: "Menu",
};

let { width = 100, height = 200, title } = options;
```

Just like with arrays or function parameters, default values can be any expression or even function calls. They’ll be evaluated if an explicit value isn’t provided.

In the code below, `prompt` asks for `width`, but not for `title`:

```JavaScript title:app.js
let options = {
	title: "Menu",
}

let {width = prompt("width?"), title = prompt("title?")} = options;
```

We also can combine both the colon and equality:

```JavaScript title:app.js
let options = {
	title: "Menu"
};

let {width: w = 100, height: h = 200, title} = options;
```

If we have a complex object with many properties, we can extract only what we need:

```JavaScript title:app.js
let options = {
	title: "Menu",
	width: 100,
	height: 200,
};

// only extract title as a variable
let { title } = options;
```

#### The rest pattern
If the object has more properties than we have variables, we can use the rest patter, just like we did with arrays. Like so:

```JavaScript title:app.js
let options = {
  title: "Menu",
  height: 200,
  width: 100
};

// title = property named title
// rest = object with the rest of properties
let {title, ...rest} = options;

// now title="Menu", rest={height: 200, width: 100}
alert(rest.height);  // 200
alert(rest.width);   // 100
```

#### Gotcha if there’s no `let`
In the examples above, variables were declared right in the assignment. Of course, we could use existing variables too, without `let`. But there’s a catch.

This won’t work:

```JavaScript title:app.js
let title, width, height;

// error in the line
{ title, width, hight } = { title: "Menu", wdith: 200, height: 100 };
```

The problem is that JavaScript treats `{...}` in the main code flow as a code block. Such code blocks can be used to group statements, like so:

```JavaScript title:app.js
{
	// a code block
	let message = "Hello";
	// ...
	alert( message );
}
```

Here, JavaScript assumes that we have a code block. We want destructuring instead.

To show JavaScript that it’s not a code block, we can wrap the expression in parentheses `(...)`:

```JavaScript title:app.js
let title, width, height;

({title, width, height} = {title: "Menu", width: 200, height: 100});

alert( title ); // Menu
```