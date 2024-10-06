### Meta
2024-10-03 21:28
**Tags:** [[javascript]] [[javascript_frameworks]] [[express.js]]
**State:** #completed 

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
