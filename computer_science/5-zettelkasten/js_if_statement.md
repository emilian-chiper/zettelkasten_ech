### Meta
2024-09-17 22:05
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_conditionals]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
let year = promtp('In which year was ECMAScript-2015 specification published?', '');

if (year == 2015) console.log( 'You are right!' );
```

### What it does
-  Evaluates a condition in parentheses and, if the result is `true`, executes a block of code.
- If we want to execute more than one statement, we have to wrap our code block into curly braces:

```JavaScript title:app.js
if (year == 2015) {
	console.log( "That's correct!" );
	console.log( "You're so smart!" );
}
```

- It is advisable to wrap the code block with curly braces `{}` every time you use an `if` statement, even if there is only one statement to execute. Doing so improves readability.