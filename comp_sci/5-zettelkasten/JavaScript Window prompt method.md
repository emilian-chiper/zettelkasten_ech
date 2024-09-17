### Meta
- - -
- 2024-09-17 07:37
- Tags: [[javascript]] [[javascript fundamentals]] [[javascript interaction]] [[Window interface]]
- Status: #completed 

### What it looks like
- - -
```JavaScript file:app.js
prompt();
prompt(message);
prompt(message, defaultValue);
```

### What it does
- - -
-  Instructs the browser to display a dialog with an optional message prompting the user to input some text, and to wait until the user either submits it or cancels the dialog.
- Under some conditions -- for example, when the user switches tabs -- the browser may not actually display a dialog, or may not wait for the user to dismiss it.

#### Parameters
- `messag`
	- Optional.
	- A string of text to display to the user. Can be omitted if there is nothing to show in the prompt window.
- `defaultValue`
	- Optional
	- A String containing the default value displayed in the text input field.

#### Return value
- A string containing the text entered by the user, or `null`.

### Examples
---
```JavaScript file:app.js
let sign = prompt("What's your sign?");

if (sign.toLowerCase() === "scorpio") {
alert("Wow! I'm a Scorpio too!");
}
```
