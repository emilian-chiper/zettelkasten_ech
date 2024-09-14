### Meta
- - -
- 2024-09-13 17:13
- Tags: [[web development]] [[frontend]] [[html]]
- Status: #completed

### What it looks like
- - -
```HTML file:index.html
<DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="./src/css/styles.css">
    <script defer src="./src/app.js"></script>
    <title>Document</title>
</head>
<body>
    <!-- code goes here -->
</body>
</html>
```

### What it does
---
- Represents the basic structure of all HTML documents.
- Must be in place before anything else can be written.

### How it does it
- - -
-  `<!DOCTYPE html>` tells the browser what document type to expect.
- The `lang` attribute specifies the language of the element's content.
- The `<head>` element is a container for metadata, which typically defines the document title, character set, styles, scripts, and other meta information.
- The `meta` tag defines metadata about an HTML document. It won't be displayed on the page, but is machine-parsable.
- The `charset` attribute specifies the character encoding for the HTML document. UTF-8 covers most of the characters and symbols in the world.
- The `viewport` meta element defines the properties of the area of the window in which web content is displayed.
- The `<link>` tag defines the relationship between a document and an external resource, usually a stylesheet.
- The `rel` attribute specifies the relationship between the current document and the linked document.
- The `href` attribute specifies the URL of the page or file the `link` tag links to, in this case, a file called `styles.css`, found in the `css` subfolder of the `src` folder in the root directory of the project.
- The `<script>` tag is used to embed a client-side JavaScript script file.
- The `defer` attribute is a boolean attribute. If set, it specifies the script is downloaded in parallel to parsing the page, and executed after the page has finished parsing.
- The `<title>` tag defines the title of the document. It is `REQUIRED`.
- The `<body>` tag defines the document's body, containing all the headings, paragraphs, images, hyperlinks, tables, links, etc.