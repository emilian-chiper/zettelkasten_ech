### Meta
2024-10-02 11:30
**Tags:** [[research]]
**Status:** #pending 

### Installing Express

#### Requirements
- `Express 4.x` requires `Node.js 0.10` or higher.
- `Express 5.x` requires `Node.js 18` or higher.

#### Steps
Create and switch to the working directory.

```BASH title:script.sh
mkdir myapp
cd myapp
```

Create `package.json` file for our application.

```BASH title:script.sh
npm init
```

This command prompts you for a number of things, such as the name and version of your application. For now, you can simply hit RETURN to accept the defaults for most of them, with the following exception:

```JSON title:package.json
entry point: (index.js)
```

Enter `app.js`, or whatever you want the name of the file to be. If you want it to be `index.js`, hit `RETURN` to accept suggested default file name.

Now install Express in the `myapp` directory and save it in the dependencies list.

```BASH script.sh
npm install express
```

### Hello world example

```JavaScript title:app.js
const express = require('express' 4.18.2)
const app = express()
const port = 3000

app.get('/', (req, res) => {
    res.send('Hello World!')
})

app.listen(port, () => {
    console.log(`Example app listending on port ${port})
})
```

#### What's going on?
This app starts a server and listens on port 3000 for connections.

The app responds with "Hello World!" for requests to the root URL (`/` ) or *route*.
For every other path, it will respond with a `404 Not Found`.

#### Running locally
Create a directory named `myapp`, change to it and run `npm init`.
Install `express` as a dependency.

In the `myapp` directory, create a file named `app.js`, and copy the code from the example above.

Run the app with `node app.js`.

### Basic routing
***Routing*** refers to determining how an application responds to a client request to a particular endpoint, which is a URI (or path) and a specific HTTP request method (GET, POST, and so on).

Each route can have one or more handler functions, which are executed when the route is matched.

#### Route definition
Route definition takes the following structure

```JavaScript title:app.js
app.METHOD(PATH, HANDLER)
```

Where:
- `app` is an instance of `express`,
- `METHOD` is an [HTTP request method], in lowercase,
- `PATH` is a path on the server,
- `HADNLER` is the function executed when the route is matched.

#### Defining simple routes
Respond with `Hello World!` on the homepage:
```JavaScript title:app.js
app.get('/', (req, res) => {
	res.send('Hello World!')
})
```

Respond to POST request on the root route (` / `), the application's home page:

```JavaScript title:app.js
app.post('/', (req, res) => {
	res.send('Got a POST request');
})
```

Respond to a PUT request to the `/user` route:

```JavaScript title:app.js
res.put('/user', (req, res) => {
	res.send('Got a PUT request at /user');
})
```

Respond to a DELETE request to the `/user` route:

```JavaScript title:app.js
app.delete('/user', (req, res) => {
	res.send('Go a DELETE request at /user')
})
```

### Routing
**Routing** refers to how an application's endpoints (URIs) respond to client requests.

You define routing using methods of the Express `app` object that correspond to HTTP methods, such as `app.get()` or `app.post()`.

You can also use `app.all()` to handle all HTTP methods, and `app.use()` to specify middleware as the callback function.

These routing methods specify a handler function called when the application receives a request to the specified route (endpoint) and HTTP method.

In other words, the app "listens" for requests that match the specified route(s) and method(s). When it detects a match, it calls the specified callback function.
Routing methods can have more than one callback function as arguments.

With multiple callbacks, it's important to provide `next` as an argument to the callback function and the call `next()` within the body of the function to hand off control to the next callback.

```JavaScript title:app.js
const express = require('express');
const app = express();

// respond with 'hello world' when a GET request is made to the homepage
app.get('/', (req, res) => {
	res.send('hello world');
})
```

#### Route methods
A route method is derived form one of the HTTP methods, and is attached to an instance of the `express` class.

```JavaScript title:app.js
// GET method route
app.get('/', (req, res) => {
	res.send('GET request to the homepage');
});

// POST method route
app.post('/', (req, res) => {
	res.send('POST request to the homepage');
});
```

#### Route paths
Rout paths, in combination with a request method, define endpoints at which requests can be made.

Route paths can be strings, string patterns, or regular expressions.
The characters `?`, `+`, `*`, and `()` are subsets of their regular expression counterparts.

The hyphen (`-`) and the dot (`.`) are interpreted literally by string-based paths.
If you need to use the dollar character (`$`) in a path string, enclose it escaped within `([` and `])`. For example, the path string for requests at `/data/$book` would be `data/([\$)]book`.

**Notes:**
- Express uses path-to-regexp for matching `route paths.
- Query strings are not part of the route path.

##### Examples of route paths based on strings
This route path will match requests to the root route, `/`.

```JavaScript title:app.js
app.get('/', (req, res) => {
	res.send('root');
});
```

This route path will match requests to `/about`.

```JavaScript title:app.js
console.log('snip');
```

This route path will match requests to `/random.text`

```JavaScript title:app.js
app.get('/random.text', (req, res) => {
	res.send('random.text')
});
```

##### Examples of route paths based on string patterns
This route path will match `acd` and `abcd`

```JavaScript title:app.js
app.get('/ab?cd', (req, res) => {
	res.send('ab?cd');
})
```

This route path will match `abcd`, `abbcd`, `abbbcd`, and so on

```JavaScript title:app.js
app.get('/ab+cd', (req, res) => {
	req.send('ab+cd');
})
```

This route path will match `abcd`, `abxcd`, `abRANDOMcd`, `ab123cd`, and so on.

```JavaScript title:app.js
app.get('/ab*cd', (req, res) => {
	res.send('ab*cd');
});
```

This route path will match `/abe` and `/abcde`.

```JavaScript title:app.js
app.get('/ab(cd)?e', (req, res) => {
	res.send('ab(cd)?e');
});
```

##### Examples of route paths based on regular expressions
This route path will match anything with an "a" in it.

```JavaScript title:app.js
app.get(/a/, (req, res) => {
	res.send('/a/');
})
```

This route path will match `butterfly` and `dragonfly`, but not `butterflyman`, `dragonflyman` and so on.

```JavaScript title:app.js
app.get(/.*fly$/, (req, res) => {
	res.send('/.*fly$/')
})
```

#### Route parameters
Route parameters are named URL segments used to capture the values specified at their position in the URL.

The capture values are populated in the `req.params` object, with the name of the route parameter specified in the path as their respective keys.

```
Route path: /user/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userID": "34", "bookId": "8989" }
```

To define routes with route parameters, simply specify the route parameters in the path of the route as shown below.

```JavaScript title:app.js
app.get('/users/:userId/books/:bookId', (req, res) => {
	res.send(req.params)
})
```

**Note:** The name of route parameters must be made of "word characters" `([A-Za-z0-9_])`.

Since the hyphen (`-`) and the dot (`.`) are interpreted literally, they can be used along with route parameters for useful purposes.

```
Route path: /flights/:from-:to
Request URL: http://localhost:3000/flights/LAX-SFO
req.params: { "from": "LAX", "to": "SFO" }
```

```
Route path: /plantae/:genus.:species
Request URL: http://localhost:3000/plantae/Prunus.persica
req.params: { "genus": "Prunus", "species": "persica" }
```

To have more control over the exact string that can be matched by a route parameter, you can append a regular expression in parentheses(`()`):

```
Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```

**Notes:**
- Because the regular expression is usually part of a literal string, be sure to escape any `\` characters with an additional backlash, for example `\\d+`.
- In Express 4.x, the `*` character in regular expression is not interpreted in the usual way. As a workaround, use `{0,}` instead of `*`.

#### Route handlers
 You can provide multiple callback functions that behave like middleware to handle a request.
 
The only exception is that these callbacks might invoke `next('route')` to bypass the remaining route callbacks.

You can use this mechanism to impose pre-conditions on a route, then pass control to subsequent routes if there's no reason to proceed with the current route.

Route handlers can be in the form of a function, an array of functions, or combinations of both, as shown in the following examples.

A single callback function can handle a route. For example:

```JavaScript title:app.js
app.get('/example/a', (req, res) => {
	res.send('Hello from A!')
})
```

More than one callback function can handle a route (make sure you specify the `next` object). For example:

```JavaScript title:app.js
app.get('/example/b', (req, res, next) => {
	console.log('the response will be sent by the next function ...')
	next()
}, (req, res) => {
	req.send('Hello from B!')
})
```

An array of callback functions can handle a route. For example:

```JavaScript title:app.js
const cb0 = function (req, res, next) {
	console.log('CB0')
	next()
}

const cb1 = function (req, res, next) {
	console.log('CB1')
	next()
}

const cb2 = function (req, res) {
	res.send('Hello from C!')
}

app.get('/example/c)', [cb0, cb1, cb2])
```

A combination of independent functions and arrays of functions can handle a route. For example:

```JavaScript title:app.js
const cb0 = function (req, res, next) {
	console.log('CB0')
	next()
}

const cb1 = function (req, res, next) {
	console.log('CB1')
	next()
}

app.get('/example/d', [cb0, cb1], (req, res, next) => {
	console.log('the response will be sent by the next function ...')
	next()
}, (req, res) => {
	res.send('Hello from D!')
})
```

#### Response methods
The methods of the response object (`res`) in the following table can send a response to the client, and terminate the request-response cycle.

If none of these methods are called from a route handler, the client request will be left hanging.

| **Method**       | **Description**                                                                       |
| ---------------- | ------------------------------------------------------------------------------------- |
| res.download()   | Prompt a file to be downloaded.                                                       |
| res.end()        | End the response process.                                                             |
| res.json()       | Send a JSON response.                                                                 |
| res.jsonp()      | Send a JSON response with JSONP support.                                              |
| res.redirect()   | Redirect a request.                                                                   |
| res.render()     | Render a view template.                                                               |
| res.send()       | Send a response a various types.                                                      |
| res.sendFile()   | Send a file as an octet stream.                                                       |
| res.sendStatus() | Set the response status code and send its string representation as the response body. |

#### app.route()
You can create chainable route handlers handlers for a route path by using `app.route()`. Because the path is specified at a single location, creating modular routes is helpful, as is reducing redundancy and typos.

Here is an example of chained route handlers that are defined by using `app.route()`.

```JavaScript title:app.js
app.route('/book')
	.get((req, res) => {
		res.send('Get a random book')
	})
	.post((req, res) => {
		res.send('Add a book')
	})
	.put((req, res) => {
		res.send('Update the book')
	})
```

#### express.Router
Use the `express.Router` class to create modular, mountable route handlers.
A `Router` instance is a complete middleware and routing system.

The following example creates a router as a module, loads a middleware function in it, defines some routes, and mounts the router module on a path in  the main app.

```JavaScript title:birds.js
const express = require('express')
const router = express.Router()

// middleware that is specific to this router
const timeLog = (req, res, next) => {
	console.log('Time:', Date.now())
	next()
}
router.use(timeLog)

// define the home page route
router.get('/', (req, res) => {
	res.send('Birds home page')
})

// define the about route
router.get('/about', (req, res) => {
	res.send('About birds')
})

module.exports = router
```

Then, load the router module in the app:

```JavaScript title:app.js
const birds = require('./birds')

// ...

app.use('/birds', birds)
```

The app will now be able to handle requests to `/birds` and `/birds/about`, as well as call the `timeLog` middleware function that is specific to the route.

If the parent route `/birds` has path parameters, it will not be accessible by default from the sub-routes. To make it accessible, you will need to pass the `mergeParams` option to the Router constructor reference.

```JavaScript title:app.js
const router = express.Router({ mergeParams: true })
```


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


### Using middleware
Express is a routing and middleware web framework that has minimal functionality of its own. An Express app is essentially a series of middleware function calls.

***Middleware*** functions are functions that have access to the *request object* (`req`), the *response object* (`res`), and the next middleware function in the application's request-response cycle. The next middleware function is commonly denoted by a variable named `next`.

Middleware functions can perform the following tasks:
- Execute any code.
- Make changes to the request and the response objects.
- End the request-response cycle.
- Call the next middleware function in the stack.

If the current middleware function does not end the request-response cycle, it must call `next()` to pass control to the next middleware function. Otherwise, the request will be left hanging.

An Express app can use the following types of middleware:
- Application-level middleware
- Router-level middleware
- Error-handling middleware
- Built-in middleware
- Third-party middleware

You can load application-level and router-level middleware with an optional mount path. You can also load a series of middleware functions together, which creates a sub-stack of the middleware system at a mount point.

#### Application-level middleware
Bind application-level middleware to an instance of the app object by using the `app.use()` and `app.METHOD()` functions, where `METHOD` is the HTTP method of the request that the middleware function handles (such as `GET`, `PUT`, or `POST`) in lowercase.

This example shows a middleware function with no mount path. The function is executed every time the app receives a request.

```JavaScript title:app.js
const express = require('express')
const app = express()

app.use((req, res, next) => {
	console.log('Time:', Date.now())
	next()
})
```

This example shows a middleware function mounted on the `/user/:id` path. The function is executed for any type of HTTP request on the `/user/:id` path.

```JavaScript title:app.js
app.use('/user/:id', (req, res, next) => {
	console.log('Request Type:', req.method)
	next()
})
```

This example shows a route and its handler function (middleware system). The function handles `GET` requests to the `/user/:id` path.

```JavaScript title:app.js
app.get('/user/:id', (req, res, next) => {
	res.send('USER')
})
```

Here's an example of loading a series of middleware functions at a mount point, with a mount path. It illustrates a middleware sub-stack that prints request info for any type of HTTP request to the `/user/:id` path.

```JavaScript title:app.js
app.use('/user/:id', (req, res, next) => {
	console.log('Request URL:', req.originalUrl)
	next()
}, (req, res, next) => {
	console.log('Request Type:', req.method)
	next()
})
```

Route handlers enable you to define multiple routes for a path. The example below defines two routes for `GET` requests to the `/user/:id` path. The second route will not cause any problems, but it will never get called because the first route ends the request-response cycle.

```JavaScript title:app.js
app.get('/user/:id', (req, res, next) => {
	console.log('ID:', req.params.id)
	next()
}, (req, res, next) => {
	res.send('User Info')
})

// handler for the /user/:id path, which prints the user ID
app.get('/user/:id', (req, res, next) => {
	res.send(req.params.id)
})
```

To skip the rest of the middleware functions from a router middleware stack, call `next('route')` to pass control to the next route.

**Note:** `next('route')` will work only in middleware functions that were loaded by using the `app.METHOD()` or `router.METHOD()` functions.

This example shows a middleware sub-stack that handles `GET` requests to the `/user/:id` path:

```JavaScript title:app.js
app.get('/user/:id', (req, res, next) => {
	// if the user ID is 0, skip to the next route
	if (req.params.id === '0') next('route')
	//otherwise pass the control to the next middleware function in this stack
	else(next)
}, (req, res, next) => {
	// send a regular response
	res.send('regular')
})

// handler for the /user/:id path, which sends a special response
app.get('/user/:id', (req, res, next) => {
	res.send('special')
})
```

Middleware can also be declared in an array for reusability.
This example shows an array with a middleware sub-stack that handles `GET` requests to the `/user/:id` path.
 
```JavaScript title:app.js
function logOriginalUrl(req, res, next) {
	console.log('Request URL:', req.originalUrl)
	next()
}

function logMethod (req, res, next) {
	console.log('Request Type:', req.method)
	next()
}

const logStuff = [logOriginalUrl, logMethod]
app.get('/user/:id', logStuff, (req, res, next) => {
	res.send('User Info')
})
```

#### Router-level middleware
Router-level middleware works in the same way as application-level middleware, except it's bound to an instance of `express.Router()`.

```JavaScript title:router.js
const router = express.Router()
```

Load router-level middleware by using the `router.use()` and `router.METHOD()` functions.

The following example code replicates the middleware system shown above for application-level middleware, by using router-level middleware:

```JavaScript title:app.js
const express = require('express')
const app = express()
const router = express.Router()

// a middleware function with no mount path. This code is executed for every request to the router
router.use((req, res, next) => {
	console.log('Time:', Date.now())
	next()
})

// a middleware sub-stack shows request info for any type of HTTP request to the /user/:id path
router.use('/user/:id', (req, res, next) => {
	console.log('Request URL:', req.originalUrl)
	next()
}, (req, res, next) => {
	console.log('Request Type:', req.method)
	next()
})

// a middleware sub-stack that handles GET requests to the /user/:id path
router.get('/user/:id', (req, res, next) => {
	// if the user ID is 0, skip to the next router
	if (req.params.id === '0') next('route')
	// otherwise pass control to the next middleware function in this stack
	else next()
}, (req, res, next) => {
	// render a regular page
	res.render('regular')
})

// handler for the /user/:id path, which renders a special page
router.get('/user/:id', (req, res, next) => {
	console.log(req.params.id)
	res.render('special')
})

// mount the router on the app
app.use('/', router)
```

To skip the rest of the router's middleware functions, call `next('router')` to pass control back out of the router instance.

This example shows a middleware sub-stack that handles `GET` requests to the `/user/:id` path.

```JavaScript title:app.js
const express = require('express')
const app = express()
const router = express.Router()

// predicate the router with a check and bail out when needed
router.use((req, res, next) => {
	if (!req.headers['x-auth']) return next('router')
	next()
})

router.get('/user/:id', (req, res) => {
	res.send('hello, user!')
})

// use the rotuer and 401 anything falling through
app.use('/amdin', router, (req, res) => {
	res.sendStatus(401)
})
```

#### Error-handling middleware
Error handling middleware always takes ***four*** arguments. You must provide four arguments to identify it as an error-handling middleware function. Even if you don't use the `next` object, you must specify it to maintain the signature. Otherwise, the `next` object will be interpreted as regular middleware and will fail to handle errors.

 Define error-handling middleware in the same way as other middleware functions, except with four arguments instead of three, specifically with the signature `(err, req, res, next)`:

```JavaScript title:app.js
app.use((err, req, res, next) => {
	console.error(err.stack)
	res.status(500).send('Something broke!')
})
```

#### Built-in middleware
Express has the following built-in middleware functions:
- `express.static` serves static assets such as HTML files, images, and so on.
- `express.json` parses incoming requests with JSON payloads.
- `express.urlencoded` parses incoming requests with URL-encode payloads.

#### Third-party middleware
Can be installed as Node.js modules.

```BASH title:script.sh
npm install cookie-parser
```

```JavaScript title:app.js
const express = require('express')
const app = express()
const cookieParser = require('cookie-parser')

// load the cookie-parsing middleware
app.use(cookieParser())
```


### Overriding the Express API
The Express API consists of various methods and properties on the request and response objects. These are inherited by prototype.

There are two extension points for the Express API:
- The global prototypes at `express.request` and `express.response`.
- App-specific prototypes at `app.request` and `app.response`.

Altering the global prototypes will affect all loaded Express apps in the same process. If desired, alterations can be made app-specific by only altering the app-specific prototypes after creating a new app.

#### Methods
You can override the signature behavior of existing methods with your own, by assigning a custom function.

Following is an example of overriding the behavior of `res.sendStatus`.

```JavaScript title:app.js
app.response.sendStatus = function (statusCode, type, message) {
	return this.contentType(type)
		.status(statusCode)
		.send(message)
}
```

The above implementation completely changes the original signature of `res.sendStatus`. It now accepts a status code, encoding type, and messages to be sent to the client.

The overridden method may now be used as follows:

```JavaScript title:app.js
res.sendSttus(404, 'application/json', '{"error":"resource not found"}'
```

#### Properties
Properties in the Express API are either:
1. Assigned properties(e.g.: `req.baseUrl`, `req.originalUrl`)
2. Defined as getters (e.g.: `req.secure`, `req.ip`)

Since properties under category 1 are dynamically assigned on the `request` and `response` objects in the context of the current request-response cycle, the behavior cannot be overridden.

Properties under category 2 can be overridden using the Express API extensions API.

The following code rewrites how the value of `req.ip` is to be derived. Now, it simply returns the value of the `Client-IP` request header.

```JavaScript title:app.js
Object.defineProperty(app.request, 'ip', {
	configurable: true,
	enumerable: true,
	get() { return this.get('Client-IP')}
})
```

#### Prototype
In order to provide the Express API, the request/response objects passed to Express (via `app(req, res)`, for example) need to inherit from the same prototype chain. By default, this is `http.IncomingRequests.prototype` for the request and `http.ServerResponse.prototype` for response.

Unless necessary, it is recommended that this be done only at the application level, rather than globally. Also, take care that the prototype that is being used matches the functionality as closely as possible to the default prototypes.

```JavaScript title:app.js
// Use FakeRequest and FakeResponse in place of http.IncomingReuest and http.ServerResponse
// for the given app reference
Object.setPrototypeOf(Object.getPrototypeOf(app.request), FakeRequest.prototype)
Object.setPrototypeOf(Object.getPrototypeOf(app.response), FakeResponse.prototype)
```

### Using template engines with Express
A ***template engine*** enables you to use static template files in your application. At runtime, the template engine replaces variables in a template file with actual values, and transforms the template into an HTML file sent to the client. This approach makes it easier to design and HTML page.

The Express application generator user Pug as its default, but supports Handlebars, EJS, etc.

To render template files, set the following application setting properties, in the default `app.js` created by the generator:
- `views`, the directory where the template files are located, e.g. `app.set('views', './views')`. This defaults to the `views` directory in the application root directory.
- `view engine`, the template engine to use, e.g. `app.set('view engine', 'pug')`.

Then, install the corresponding template engine:

```BASH title:script.sh
npm install pug --save
```

Express-compliant template-engines like Pug export a function named `__express(filePath, options, callback)`, which `res.render()` calls to render the template code.

After the view engine is set, you don't have to specify the engine or load the template engine module in your app. Express loads the module internally, e.g.:

```JavaScript title:app.js
app.set('view engine', 'pug')
```

The, create a Pug template file named `index.pug` in the `views` directory, with the following content:

```JavaScript title:index.pug
html
	head
		title=title
	body
		h1=message
```

Create a route to render the `index.pug` file. If the `view engine` property is not set, you must specify the extension of the `view` file. Otherwise, you can omit it.

```JavaScript title:app.js
app.get('/', (req, res) => {
	res.render('index', { title: 'Hey', message: 'Hello there!' })
})
```

When you make a request to the home page, the `index.pug` file will be rendered as HTML.

The view engine cache does not cache the contents of the template's output, only the underlying template itself. The view is still re-rendered with every request even when the cache is on.

### Error Handling
***Error Handling*** refers to how Express catches and processes errors that occur both synchronously and asynchronously. Express comes with a default error handler so you don't need to write your own to get started.

#### Catching Errors
