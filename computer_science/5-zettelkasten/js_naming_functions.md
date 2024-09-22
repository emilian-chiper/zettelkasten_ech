### Meta
2024-09-18 15:26
**Tags:** [[javascript]] [[javascript_fundamentals]] [[javascript_functions]]
**State:** #completed  

### What it looks like
```JavaScript title:app.js
showMessage(..) // shows a message
getAge(..) // returns the age (gets it somehow)
calcSum(..) // calculates a sum and returns the result
createForm(..) // creates a form (and usually returns it)
checkPermission(..) // checks a permission, returns true/false
```

### How it does it
- Functions are actions, so their name is usually a verb.
- It should be brief, as accurate and descriptive as possible.

#### One function - one action
- A function should do exactly what is suggested by its name, no more.
- Two independent actions usually deserve two functions, even if they are usually called together.
- Examples:
	- `getAge` would be bad if it shows an `alert` with the age (should only `get`).
	- `createForm` would be bad if it modifies the document, adding a form to it (should only `create` it and `return`).
	- `checkPermission` would be bad if it displays the `access granted/denied` message (should only perform the `check` and `return` the result.)

#### Ultrashort function names
- Functions that are used *very often* sometimes have ultrashort names.
- These are exceptions. Generally, function names should be concise and descriptive.

#### Functions === Comments
- Functions should be short and do exactly one thing.
- If that thing is big, maybe it's worth splitting the function into a few smaller functions.
- A separate function isn't only easier to test and debug -- its very existence isa great comment!

```JavaScript title:app.js
function showPrimes(n) {
	nextPrime: for (let i = 2; i < n; i++) {
		for (let j = 2; j < i; j++) {
			if (i % j == 0) continue nextPrime;
		}
	alert(i); // a prime
	}
}
```

```JavaScript title:app.js
function showPrimes(n) {
	for (let i = 2; i < n; i++) {
		if (!isPrime(i)) continue;
		alert(i);
	}
}

function isPrime(n) {
	for (let i = 2; i < n; i++) {
		if (n % i == 0) return false; 
	}
	return true;
}
```

- The functions above achieve the same objective.
- The first uses a label, the other calls another function called `isPrime` on each number from `2` to `n`.
- The difference is that the second is easier to understand.