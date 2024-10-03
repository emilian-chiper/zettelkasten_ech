### Meta
2024-10-03 21:40
**Tags:** [[javascript]] [[javascript_frameworks]] [[express.js]]
**State:** #completed 

### Writing middleware for use in Express apps

#### Overview
***Middleware*** functions are functions that have access to the *request object* (`req`), the *response object* (`res`), and the `next` function in the application's request-response cycle.

The `next` function is a function in the Express router which, when invoked, executes the middleware.

Middleware functions can perform the following tasks
- Execute any code.
- Make changes to the request and the response objects.
- End the request-response cycle.
- Call the next middleware in the stack.

If the current middleware functions doesn't end the req-res cycle, it must call `next()` to pass control to the next middleware function. Otherwise, the request will be left hanging.

#### Example
Here is an example of a simple "Hello World" Express application.
We will define and add three middleware functions to the application:
- `myLogger`, which prints a simple log message,
- `requestTime`, which displays the timestamp of the HTTP request,
- `validateCookies`, which validates incoming cookies.

```JavaScript title:app.js
const express = require('express')
const app = express()

app.get('/', (req, res) => {
	req.send('Hello World!')
})

app.listen(3000)
```

##### Middleware function myLogger
This function prints 'LOGGED' when a request to the app passes through it.
The middleware function is assigned to a variable named `myLogger`.

```JavaScript title:app.js
const myLogger = function (req, res, next) {
	console.log('LOGGED')
	next()
}
```

**Notes:**
- Notice the call above to `next()`.
- Calling this function invokes the next middleware function in the app.
- The `next()` function ins't part of the Node.js or Express API, but is the third argument that is passed to the middleware function.
- The `next()` function could be named anything, but by convention it's always named 'next'.
- To avoid confusion, always use this convention.

To load the middleware function, call `app.use`, specifying the middleware function.

```JavaScript title:app.js
const express = require('express')
const app = express()

const myLogger = function (req, res, next) {
	console.log('LOGGED')
	next()
}

app.use(myLogger)

app.get('/', (req, res) => {
	res.send('Hello World!')
})

app.listen(3000)
```

Each time the app receives a request, it prints the message "LOGGED" to the terminal.

The order of middleware loading is important: middleware functions that are loaded first are also executed first.

If `myLogger` is loaded after the route to the root path, the request never reaches it and the app doesn't print "LOGGED", because the route handler of the root path terminates the request-response cycle.

The middleware function `myLogger` simply prints a message, then passes on the request to the next middleware function in the stack calling the `next()` function.

##### Middleware function requestTime
Next, we'll create a middleware function called "requestTime" and add a property called `requestTime` to the request object.

```JavaScript title:app.js
const requestTime = function (req, res, next) {
	req.requestTime = Date.now()
	next()
}
```

The app now uses the `requestTime` middleware function. Also, the callback function of the root path route uses the property that the middleware function adds to `req` (the request object).

```JavaScript title:app.js
const express = require('express')
const app = express()

const requestTime = function (req, res, next) {
	req.reqTime = Date.now()
	next()
}

app.use(requestTime)

app.get('/', (req, res) => {
	let responseText = 'Hello world!<br>'
	responseText += `<small>Reuqested at: ${req.requestTime}</small>`
	res.send(responseText)
})

app.listen(3000)
```

When you make a request to the root of the app, the app now displays the timestamp of your request in the browser.

##### Middleware function validateCookies
Finally, we create a middleware function that validates the incoming cookies and sends a 400 response if cookies are invalid.

```JavaScript title:app.js
async function cookieValidator (cookies) {
	try {
		await externallyValidateCookie(cookies.testCookie)
	} catch {
		throw new Error('Invalid cookies')
	}
}
```
\
Here, we use the `cookie-parser` middleware to parse incoming cokkies off the `req` object and pass them to our `cookieValidator` function.

The `validateCookies` middleware returns a Promise that upon rejection will automatically trigger the error handler.

```JavaScript title:app.js
const express = require('express')
const cookieParser = require('cookie-parser')
const cookieValidator = require('./cookieValidator')

const app = express()

async function validateCookies (req, res, next) {
	await cookieValidator(req.cookies)
	next()
}

app.use(cookieParser())

app.use(validateCookies)

// error handler
app.use((err, req, res, next) => {
	res.status(400).send(err.message)
})

app.listen(3000)
```

**Notes:**
- Note how `next()` is called after `await cookieValidator(req.cookies)`.
- This ensures that if `cookieValidator` resolves, the next middleware in the stack will get called.
- If you pass anything to the `next()` function (except the string `route` or `router`), Express regards the current request as being an error and will skip any remaining non-error handling routing and middleware functions.

Because you have access to the request object, the response object, the next middleware function in the stack, and the whole Node.js API, the possibilities with middleware functions are endless.

#### Configurable middleware
If you need middleware to be configurable, export a function which accepts an options object or other parameters, which then returns the middleware implementation based on the input parameters.

```JavaScript title:my-middleware.js
module.exports = function (options) {
	return function (req, res, next) {
		// Imnplement the middleware function based on the options object
		next()
	}
}
```

The middleware can now be used.

```JavaScript title:app.js
const mw = require('./my-middleware.js')

app.use(mw({ option1: '1', option2: '2' }))
```