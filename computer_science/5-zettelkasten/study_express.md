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
It's important to ensure that Express catches all errors that occur while running route handlers and middleware.

Errors that occur in synchronous code inside route handlers and middleware require no extra work. If synchronous code throws an error, then Express will catch and process it. For example:

```JavaScript title:app.js
app.get('/', (req, res) => {
	throw new Error('BROKEN') // Express will catch this on its own
})
```

For errors returned from asynchronous functions invoked by route handlers and middleware, you must pass them to the `nex()` function, where Express will catch and process them. For example:

```JavaScript title:app.js
app.get('/', (req, res, next) => {
	fs.readFile('/file-does-not-exist', (err, data) => {
		if (err) {
			next(err) // Pass errors to Express.
		} else {
			res.send(data)
		}
	})	
})
```

Starting with Express 5, route handlers and middleware that return a Promise call `next(value)` automatically when they reject or throw an error. For example:

```JavaScript title:app.js
app.get('user/:id', async (req, res, next)) {
	const user = await getUserById(req.params.id)
	res.send(user)
}
 ```

If `getUserById` throws an error or rejects, `next` will be called with either the thrown error or the rejected value. If no rejected value is provided, `next` will be called with a default Error object provided by the Express router.

If you pass anything to the `next()` function (except the string `'route'`), Express regards the current request as being an error and will skip any remaining non-error handling routing and middleware functions.

If the callback in a sequence provides no data, only errors, you can simplify this code as follows:

```JavaScript title:app.js
app.get('/', [
	function (req, res, next) {
		fs.writeFile('/inaccessible-path', 'data', next)
	},
	function (req, res) {
		res.send('OK')
	}
])
```

In the above example, `next` is provided as the callback for `fs.writeFile`, which is called with or without errors. If there's no error, the second handler is executed, otherwise Express catches and processes the error.

You must catch errors that occur in asynchronous code invoked by route handlers or middleware and pass them to Express for processing. For example:

```JavaScript title:app.js
app.get('/', (req, res, next) => {
	setTimeout(() => {
		try {
			thrown new Error('BROKEN')
		} catch (err) {
			next(err)
		}
	}, 100)
})
```

The above example uses a `try ... catch` block to catch errors in the asynchronous code and pass them to Express. If the `try ... catch` block were omitted, Express would not catch the error since it is not part of the synchronous handler code.

Use promises to avoid the overhead of the `try ... catch` block or when using functions that return promises. For example:

```JavaScript title:app.js
app.get('/', (req, res, next) => {
	Promise.resolve().then(() => {
		throw new Error('BROKEN')
	}).catch(next) // Errors will be passed to Express.
})
```

Since promises automatically catch both synchronous errors and rejected promises, you can simply provide `next` as the final catch handler and Express will catch errors, because the catch handler is given the error as the first argument.

You could also use a chain of handlers to rely on synchronous error catching, by reducing the asynchronous code to something trivial. For example:

```JavaScript title:app.js
app.get('/', [
	function (req, res, next) {
		fs.readFile('/maybe-valid-file', 'utf-8', (err, data) => {
			res.locals.data = data
			next(err)
		})
	},
	function (req, res) {
		res.locals.data = res.locals.data.split(',')[1]
		res.send(res.locals.data)
	}
])
```

The above example has a couple of trivial statements from the `readFile` call. If `readFile` causes an error, the it passes the error to Express, otherwise you quickly return to the world of synchronous error handling in the next handler in the chain. Then, the example tries to process the data. If this fails, then the synchronous error  handler will catch it. If you had done the processing inside the `readFile` callback, then the application might exit and the Express error handlers would not run.

Whichever method you use, if you want Express error handlers to be called in and the application to survive, you must ensure that Express receives the error.

#### The default error handler
Express comes with a built-in error handler that takes care of any errors that might be encountered in the app. This default error-handling middleware function is added at the end of the middleware function stack.

If you pass an error to `next()` and you do not handle it in the custom error handler, it will be handled by the built-in error handler; the error will be written to the client with the stack trace. The stack trace is not included in the production environment.

**Note:** Set the environment variable `NODE_ENV` to `production`, to run the app in production mode.

When an error is written, the following information is added to the response:
- The `res.statusCode` is set from `err.status` (or `err.statusCode`. If this value is outside the `4xx` or `5xx` range, it will be set to `500`.
- The `res.statusMessage` is set according to the status code.
- The body will be the HTML of the status code message when in production environment, otherwise will be `err.stack`.
- Any headers specified in an `err.headers` object.

If you call `next()` with an error after you have started writing the response (for example, if you encounter an error while streaming the response to the client), the Express default error handler closes the connection and fails the request.

So, when you add a custom error handler, you must delegate to the default Express error handler, when the headers have already been sent to the client:

```JavaScript title:app.js
function erroHandler(err, req, res, next) {
  if (res.headersSent) {
    return next(err)
  }
  res.status(500)
  res.render('error', { error: err })
}
```

Note that the default error handler can get triggered if you call `next()` with an error in your code more than once, even if custom error handling middleware is in place.

#### Writing error handlers
Define error-handling middleware functions in the same way as other middleware functions, except error-handling functions have four arguments instead of three: `(err, req, res, next)`. For example:

```JavaScript title:app.js
app.use((err, req, res, next) => {
	console.error(err.stack)
	res.status(500).send('Something broke!')
})
```

You define error-handling middleware last, after other `app.use()` and routes calls; for example:

```JavaScript title:app.js
const bodyParser = require('body-parser')
const methodOverrider = reuire('method-override')

app.use(bodyParser.urlencoded({
	extended: true
}))
app.use(bodyParser.json())
app.use(methodOverride())
app.use((err, req, res, next) => {
	// logic
})
```

Responses from within a middleware function can be in any format, such as an HTML error page, a simple message, or a JSON string.

For organizational (and higher-level framework) purposes, you can define several error-handling middleware functions, much as you would with regular middleware functions. For example, to define an error-handler for requests made by using `XHR` and those without:

```JavaScript title:app.js
const bodyParser = require('body-parser')
const methodOverrride = require('method-override')

app.use(bodyParser.urlencoded({
  extended: true
}))
app.use(bodyParser.json())
app.use(methodOverride())
app.use(logErrors)
app.use(logErrors)
app.ue(clientErrorHandler)
app.use(errorHandler)
```

In this example, the generic `logErrors` might write request and error information to `stderr`, for example:

```JavaScript title:app.js
function logErrors (err, req, res, next) {
	console.error(err.stack)
	next(err)
}
```

Also in this example, `clientErrorHandler` is defined as follows.

```JavaScript title:app.js
function clientErrorHandler (err, req, res, next) {
	if (req.xhr) {
		req.status(500).send({ error: 'Something failed!' })
	} else {
		next(err)
	}
}
```

In this case, the error is explicitly passed along to the next one.

Notice that when ***not*** calling "next" in an error-handling function, you are responsible for writing (and ending) the response. Otherwise, those requests will "hang" and will not be eligible for garbage collection.

Implement the "catch-all" `errorHandler` function as follows:

```JavaScript title:app.js
function errorHandler (err, req, res, next) {
	res.status(500)
	res.render('error', { error: err })
}
```

If you have a route handler with multiple callback functions, you can use the `route` parameter to skip to the next route handler. For example:

```JavaScript title:app.js
app.get('/a_route_behind_paywall',
  (req, res, next) => {
	  if (!req.user.hasPaid) {
	    // continue handling this request
	    next('route')
	  } else {
	    next()
	  }
  }, (req, res, next) => {
    PaidContent.find((err, doc) => {
      if (err) return next(err)
      res.json(doc)
    })
  }
)
```

In this example, the `getPaidContent` handler will be skipped but any remaining handlers in `app` for `/a_route_behind_paywall` would continue to be executed.

**Note:** Calls to `next()` and `next(err)` indicate that the current handler is complete and in what state. `next(err)` will skip all remaining handlers in the chain except for those that are set up handle errors as described above.

### Debugging Express
To see all the internal logs used in Express, set the `DEBUG` environment variable to `express:*` when launching your app.

```BASH title:debug_express.sh
DEBUG=express:* node index.js
```

Running the command on the default app generated by the express generator prints the following output:

```BASH title:debug_express.sh
DEBUG=express:* node ./bin/www
  express:router:route new / +0ms
  express:router:layer new / +1ms
  express:router:route get / +1ms
  express:router:layer new / +0ms
  express:router:route new / +1ms
  express:router:layer new / +0ms
  express:router:route get / +0ms
  express:router:layer new / +0ms
  express:application compile etag weak +1ms
  express:application compile query parser extended +0ms
  express:application compile trust proxy false +0ms
  express:application booting in development mode +1ms
  express:router use / query +0ms
  express:router:layer new / +0ms
  express:router use / expressInit +0ms
  express:router:layer new / +0ms
  express:router use / favicon +1ms
  express:router:layer new / +0ms
  express:router use / logger +0ms
  express:router:layer new / +0ms
  express:router use / jsonParser +0ms
  express:router:layer new / +1ms
  express:router use / urlencodedParser +0ms
  express:router:layer new / +0ms
  express:router use / cookieParser +0ms
  express:router:layer new / +0ms
  express:router use / stylus +90ms
  express:router:layer new / +0ms
  express:router use / serveStatic +0ms
  express:router:layer new / +0ms
  express:router use / router +0ms
  express:router:layer new / +1ms
  express:router use /users router +0ms
  express:router:layer new /users +0ms
  express:router use / &lt;anonymous&gt; +0ms
  express:router:layer new / +0ms
  express:router use / &lt;anonymous&gt; +0ms
  express:router:layer new / +0ms
  express:router use / &lt;anonymous&gt; +0ms
  express:router:layer new / +0ms
```

When a request is then made to the app, you will see the logs specified in the Express code:

```BASH title:debug_express.sh
    express:router dispatching GET / +4h
  express:router query  : / +2ms
  express:router expressInit  : / +0ms
  express:router favicon  : / +0ms
  express:router logger  : / +1ms
  express:router jsonParser  : / +0ms
  express:router urlencodedParser  : / +1ms
  express:router cookieParser  : / +0ms
  express:router stylus  : / +0ms
  express:router serveStatic  : / +2ms
  express:router router  : / +2ms
  express:router dispatching GET / +1ms
  express:view lookup "index.pug" +338ms
  express:view stat "/projects/example/views/index.pug" +0ms
  express:view render "/projects/example/views/index.pug" +1ms
```

To see the logs only from the router implementation, set the value of `DEBUG` to `express:router`. Likewise, to see logs only from the application implementation, set the value of `DEBUG` to `express:application`, and so on.

#### Applications generated by `express`
An app generated by the `express` command uses the `debug` module and its debug namespace is scoped to the name of the app.

For example, if you generated the app with `$ express sample-app`, you can enable the debug statements with the following command:

```BASH title:debug_express.sh
DEBUG=sample-app:* node ./bin/www
```

You can specify more than one debug namespace by assigning a comma-separated list of names:

```BASH title:debug_express.sh
DEBUG=http,mail,express:* node index.js
```

#### Advanced options
When running through Node.js, you can set a few environment variables that will change the behavior of the debug logging.


| **Name**            | **Purpose**                                      |
| ------------------- | ------------------------------------------------ |
| `DEBUG`             | Enables/disables specific debugging namesapces.  |
| `DEBUG-COLORs`      | Whether or not to use colors in the debug output |
| `DEBUG-DEPTH`       | Object inspection depth.                         |
| `DEBUG_FD`          | File descriptor to write debug output to.        |
| `DEBUG_SHOW_HIDDEN` | Shows hidden properties on inspected objects.    |

**Note:** The environment variables beginning with `DEBUG_` end up being converted into an Options object that gets used with `%o` / `%0` formatters. See the Node.js docs for `util.inspect()` for the complete list.

### Express behind proxies
When running an Express app behind a reverse proxy, some of the Express APIs may return different values than expected. In order to adjust for this, the `trust proxy` application setting may be used to expose information provided by the reverse proxy in the Express APIs. The most  common issue is express APIs that expose the client's IP address may instead show an internal IP address of the reverse proxy.

**Note:** When configuring the `trust proxy` setting, it is important to understand the exact setup of the reverse proxy. Since the setting will trust values provided in the request, it is important that the combination of the setting in Express matches how the reverse proxy operates.

The application setting `trust proxy` may be set to one of the values listed bellow.

##### Boolean
If `true`, the client's IP address is understood as the left-most entry in the `X-Forwarded-For` header.

If `false`, the app is understood as directly facing the client and the client's IP address is derived from `req.socket.remoteAddress`. This is the default setting.

**Warning!** When setting to `true`, it is important to ensure that the last reverse proxy trusted is removing/overwriting all of the following HTTP headers: `X-Forwarded-For`, `X-Forwarded-Host`, and `X-Forwarded-Proto`, otherwise it may be possible for the client to provide any value.

##### IP addresses
An IP address, subnet, or an array of IP addresses and subnets to trust as being a reverse proxy. The following list shows the pre-configured subnet names:
- loopback - `127.0.0.1/8`, `::1/128`
- linklocal - `169.254.0.0/16`, `fe80::/10`
- uniquelocal - `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `fc00::/7`

You can set IP addresses in any of the following ways:

```JavaScript title:app.js
app.set('trust proxy', 'loopback') // specify a single subnet
app.set('trust proxy', 'loopback, 123.123.123.123') // specify a subnet and an address
app.set('trust proxy', 'loopback, linklocal, uniquelocal') // specify multiple subnets as CSV
app.set('trust proxy', ['loopback', 'linklocal', 'uniquelocal']) // specify multiple subnets as an array
```

When specified, the IP addresses or the subnets are excluded from the address determination process, and the untrusted IP address nearest to application server is determined as the client's IP address. This works by checking if `req.socket.remoteAddress` is trusted. If so, then each address in `X-Forwarded-For` is checked from right to left until the first non-trusted address.

##### Number
Use the address that is at most `n` number of hops away from the Express application. `req.socket.remoteAddress` is the first hop, and the rest are looked for in the `X-Forwarded-For` header from right to left. A value of `0` means that the first untrusted address would be `req.socket.remoteAddress`, i.e. there is no reverse proxy.

**Warning!** When using this setting, it is important to ensure there are not multiple, different-length paths to the Express app such that the client can be less than the configured number of hops away, otherwise it may be possible for the client to provide any value.

##### Function
Custom trust implementation.

```JavaScript title:app.js
app.set('trust proxy', (ip) => {
  if (ip === '127.0.0.1' || ip === '123.123.123.123') return true // truste IPs
  else return false
})
```


Enabling `trust proxy` will have the following impact:
- The value of `req.hostname` is derived from the value set in the `X-Forwarded-Host` header, which can be set by the client or by the proxy.
- `X-Forwarded-Proto` can be set by the reverse proxy to tell the app whether it is `https` or `http` or even an invalid name. This value is reflected by `req.protocol`.
- The `req.ip` and `req.ips` values are populated based on the socked address and `X-Forwarded-For` header, starting at the first untrusted address.

The `trust proxy` setting is implemented using the `proxy-addr` package (see docs).

### PostgreSQL database integration
**Module:** `pg-promise`
**Installation**
`$ nmp install pg-promise`

**Example**
```JavaScript title:app.js
const pgp = require('pg-promise')(/* options */)
const dp = pgp('postgress://username:password@host:port/database')

db.one('SELECT $1 AS value', 123)
  .then((data) => {
    console.log('DATA:', data.value)
  })
  .catch((error) => {
    console.log('ERROR:', error)
  })
```