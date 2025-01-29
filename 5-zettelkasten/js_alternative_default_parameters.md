### Meta
2024-09-18 15:07
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_functions]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
function showMessage(text) {
	// ...
	if (text === undefined) {
		text = 'empty message';
	}
}
```

```JavaScript title:app.js
function showMessage(text) {
	text = text || 'empty';
}
```

```JavaScript title:app.js
function showCount(count) {
	console.log(count ?? "unknown");
}

showCount(0); // 0
showCount(null); // unknown
showCount(); // unknown
```
