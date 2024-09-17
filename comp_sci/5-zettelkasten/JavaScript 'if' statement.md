### Meta
- - -
- 2024-09-17 10:47
- Tags: [[javascript]] [[javascript conditionals]]
- Status: #completed 

### What it looks like
- - -
```JavaScript file:app.js
let year = promtp('In which year was ECMAScript-2015 specification published?', '');

if (year == 2015) console.log( 'You are right!' );
```

### What it does
- - -
-  Evaluates a condition in parentheses and, if the result is `true`, executes a block of code.
- If we want to execute more than one statement, we have to wrap our code block into curly braces:

```JavaScript file:app.js
if (year == 2015) {
	console.log( "That's correct!" );
	console.log( "You're so smart!" );
}
```

- It is advisable to wrap the code block with curly braces `{}` every time you use an `if` statement, even if there is only one statement to execute. Doing so improves readability.