### Meta
2024-09-20 08:08
**Tags:** [[javascript]] [[javascript_object_basics]] [[javascript_optional_chaining]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let user = {};

alert(user.address.street); // error
```

### What happens
- As `user.address` is `undefined`, an attempt to get `user.address.street` fails with an error.

### How it does it
- In many practical cases we'd prefer to get `undefined` instead of an error (meaning 'no street').

### Another example
```JavaScript title:app.js
let html = document.querySelector('.elem').innerHTML; // error if it's null
```

- If the element doesn't exist, we'll get an error accessing `innerHTML` property of `null`.
- In some cases, when the absence of the element is normal, we'd like to avoid the error and just accept `html = null` as the result.
- The obvious solution would be to check the value using `if` or the conditional operator `?`, before accessing its property, like this:

```JavaScript title:app.js
let user = {};

alert(user.address ? user.address.street : undefined);
```

- It works, there's no error, but it's rather inelegant.
- Here's how the same would look for `document.querySelector`:

```JavaScript title:app.js
let html = document.querySelector('.elem')
	? document.querySelector('.elem').innerHTML
	: null;
```

- We can see that the element search `document.querySelector('.elem')` is actually called twice here. Not good.
- For more deeply nested properties, it becomes even uglier, as more repetitions are required.
- For example, let's get `user.address.street.name`:

```JavaScript title:app.js
let user = {};

alert(user.address ? user.address.street ? user.address.street.name : null : null);
```

- There's a slightly better way to write it, using the `&&` operator:

```JavaScript title:app.js
let user = {};

alert( user.address && user.address.street && user.address.street.name ); // undefined (no error)
```

- AND'ing the whole path to the property ensures that all components exist. If not, the operation stops.
- This is also not ideal.
- That is why optional chainging `?.` was added to the language.