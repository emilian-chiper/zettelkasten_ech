### Meta
- - -
- 2024-09-15 21:05
- Tags: [[html]] [[html elements]] [[html metadata]]
- Status: #completed 

### What it looks like
- - -
```HTML file:index.html
<base targe="_top" href="https://www.example.com/" />
```

### What it does
- - -
- Specifies the base URL to use for all *relative* URL's in a document.
- There can only be only one `base` element in a document.

### Attributes
---
- `href`
	- The base URL to be used throughout the document for relative URLs.
	- Absolute and relative URLs are allowed.
	- `dat:` and `javascript:` URLs are not allowed.
- `target`
	- A **keyword** or **author-defined name** of the default [[browsing context]] to show the results of navigation from `<a>`, `<area>`, or `<form>` elements without explicit `target`  attributes.
	- The following keywords have special meanings:
		- `_self` (default): Show the result in the current browsing context.
		- `_blank`: Show the result in a new, unnamed browsing context.
		- `_parent`: Show the result in the parent browsing context of the current one, if the current page is inside a frame. If there is no parent, acts the same as `_self`.
		- `_top`: Show the result in the topmost browsing context (the browsing context that is an ancestor of the current one and has no parent). If there is no parent, acts the same as `_self`.