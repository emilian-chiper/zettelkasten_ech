### Meta
2024-09-17 22:19
**Tags:** [[javascript]] [[javascript_fundamentals]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let message;
```

### What it is
-  A `variable` is a 'named storage' for data.
- In other words, a `variable` is an identifier for a memory space containing a certain type of data.

### Assignment
- To assign this identifier to a [[data type]], use the assignment operator `=`.

```JavaScript title:app.js
let message;
message = 'Hello!';
```

- In this example, the identifier message is assigned to `Hello`, an instance of the `String` class.
- To be concise, declaration and assignment can be combined into a single line.

```JavaScript title:app.js
let message = 'Hello!';
```

- We can also declare multiple variables in one line, but it is considered a bad practice.

```JavaScript title:app.js
let user = 'John', age = 25, message = 'Hello';
```

- The multiline variant is a bit longer, but easier to read:

```JavaScript title:app.js
let user = 'John';
let age = 25;
let message = 'Hello';
```

- This style is also viable:

```JavaScript title:app.js
let user = 'John',
	age = 25,
	message = 'Hello';
```

### Reassignment
```JavaScript title:app.js
let message;
message = 'Hello';
message = 'World!';
```

- When the value is changed, the identifier is pointing to another space in memory where `'World!'`, another instance of the `String` class is created.
- We can also declare two variables and copy data from one into the other.

```JavaScript title:app.js
let hello = 'Hello world!';

let message;

/*
  Copies 'Hello world' from hello into message
  In actuality, message becomes an alias for hello
**/
message = hello
```

### Double declaration
- Declaring twice triggers a [[js_SyntaxError]].

```JavaScript title:app.js
let message = "This";

let message = "That"; // SyntaxError: 'message' has already been declared
```

### Naming conventions
- Examples of **valid** names:

```JavaScript title:app.js
let userName; // this is also known as camelCase
let test123;
let $ = 1;
let _ = 2;
```

- Examples of **invalid** names:

```JavaScript title:app.js
let 1a; // cannot start with a digit

let my-name; // hyphens aren't allowed
```

- **Note:** Case matters -- `apple` and `APPLE` are two different variables.
- **Note:** Non-Latin letters are allowed, but not recommended.
- There are also a number of [[reserved words]] that cannot be used as identifiers for variables.

#### Best practices
- Use human-readable names like `userName` or `shoppingCart`.
- Stay away from abbreviations or short names like `a`, `b`, and `c`, unless you know what you're doing.
- Make names maximally descriptive and concise. Examples of bad names are `data` and `value`. Such names say nothing. Their use is permitted if the context of the code makes it exceptionally clear which data or value the variable is referencing.
- Agree on naming conventions with your collaborators.

### Constants
- To declare a constant, use the keyword `const`.

```JavaScript title:app.js
const myBirthday = '18.04.1982';
```

- Variables declared using `const` are called **constants**.
- They cannot be reassigned. Attempting to do so throws an error.

#### Uppercase constants
- There is a widespread practice to use constants as aliases for difficult-to-remember values that are known before execution.
- Such constants are named using capital letters and underscores.

```JavaScript title:app.js
const COLOR_ORANGE = '#FF7F00';

let color = COLOR_ORANGE;
```

- Benefits
	- `COLOR_ORANGE` is much easier to remember than `#FF7F00`.
	- It's much easier to mistype `#FF7F00` than `COLOR_ORANGE`.
	- When reading the code, `COLOR_ORANGE` is much more meaningful than `#FF7F00`
