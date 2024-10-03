### Meta
2024-10-03 21:44
**Tags:** [[javascript]] [[javascript_frameworks]] [[express.js]]
**State:** #completed 

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