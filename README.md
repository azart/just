# JUST

JavaScript template engine.

## Installation

	npm install just

## Features

  * Caching templates
  * Automatic reloading of changed templates
  * JavaScript code in templates
  * Supports tag customization
  * Node.JS and client-side support
  * Powerful but simple syntax
  * Inheritance, partials, blocks

## Usage

```js
var JUST = require('just');

var just = new JUST({ root : __dirname + '/view' });

just.render('page', { title: 'Hello, World!' }, function(error, html) {
	console.log(error);
	console.log(html);
});
```

You may use JavaScript object as root.

```js
var JUST = require('just');

var just = new JUST({ root : {
				layout: '<html><head><title><%- title %></title></head><body><%*%></body></html>',
				page: '<%! layout %><p>Page content</p>'
				}
			});

just.render('page', { title: 'Hello, World!' }, function(error, html) {
	console.log(error);
	console.log(html);
});
```

See full example in [examples](https://github.com/baryshev/just/tree/master/examples) folder.

## Syntax

### Output

```
<%- someVar %>
```

### JavaScript code

```
<% for (var i = 0; i < articles.length; i++) { %>
<% this.partial('article', { article: articles[i] }); %>
<% } %>
```

or

```
<% if (user.authenticated) { %>
<%@ partials/user %>
<% } else { %>
<%@ partials/auth %>
<% } %>
```

### Inheritance

```
<%! layout %>
```
or 

```
<% this.extend('layout', { customVar: 'Hello, World!' }); %>
```

Use


```
<%*%>
```

or

```
<% this.child(); %>
```

in parent template to define the insertion point.

### Partials

```
<%@ partial %>
```

or

```
<% this.partial('partial', { customVar: 'Hello, World!' }); %>
```

### Blocks

```
<%[ blockName %>
<p>This is block content</p>
<%]%>
```

or

```
<% this.blockStart('blockName'); %>
<p>This is block content</p>
<% this.blockEnd(); %>
```

Use


```
<%* blockName %>
```

or

```
<% this.child('blockName'); %>
```

in parent template to define the insertion point.

Blocks supports more than one level of inheritance and may be redefined.

## Options

  - `root`            Templates root folder or JavaScript object containing templates
  - `ext`             Extension of templates, defaulting to '.html' (not used for JavaScript objects as root)
  - `useCache`        Compiled functions are cached, defaulting to true
  - `watchForChanges` Automatic reloading of changed templates, defaulting to false (useful for debugging, not supported for client-side)
  - `open`            Open tag, defaulting to '<%'
  - `close`           Closing tag, defaulting to '%>'

## Client-side support

Basically, include [just.min.js](https://github.com/baryshev/just/tree/master/just.min.js) to a page and JUST ready to use.

```js
var just = new JUST({ root : '/view' });

just.render('page', { title: 'Hello, World!' }, function(error, html) {
	console.log(error);
	console.log(html);
});
```

NOTE: root folder must be on the same domain to avoid cross-domain restrictions.

## License 

(The MIT License)

Copyright (c) 2012 Vadim M. Baryshev &lt;vadimbaryshev@gmail.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
