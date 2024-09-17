### Meta
- - -
- 2024-09-16 22:40
- Tags: [[javascript]] [[javascript fundamentals]] [[javascript interaction]] [[Window interface]]
- Status: #completed 

### What it looks like
- - -
```JavaScript file:app.js
alert()
alert(message)
```

### What it does
- - -
-  `window.alert()` instructs the browser to display a dialog with an optional message, and to wait until the user dismisses the dialog.
- Under some conditions -- for example, when the user switches tabs -- the browser may not actually display a dialog, or may not wait for the user to dismiss it.

#### Parameters
- `message`
	- Optional.
	- A string you want to display in the alert dialog, or
	- An object that is converted into a string and displayed.

#### Return value
- `undefined`

### Examples
---
```JavaScript file:app.js
window.alert("Hello world!");
alert("Hello world!");
```
