### Meta
2024-10-03 21:43
**Tags:** [[javascript]] [[javascript_frameworks]] [[express.js]]
**State:** #completed 

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