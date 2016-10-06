# webpack-session
webpack-session



# Webpack
https://webpack.github.io/

Webpack is module bundler. Modules in require statement and we can load a single file in the page.

![alt text](https://webpack.github.io/assets/what-is-webpack.png "Logo Title Text 1")


At present:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Webpack Session</title>
    <script src="one.js"></script>
    <script src="two.js"></script>
    <script src="three.js"></script>
</head>
<body>

</body>
</html>
```

Or One file depends on others otherwise does not work. Like - 


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Webpack Session</title>
    <script src="one.js"></script>
    <script src="three.js"></script>
    <script src="two.js"></script>
</head>
<body>

</body>
</html>
```


Webpack solution, load only a single file and webpack will handle everything -

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Webpack Session</title>
    <script src="bundle.js"></script>
</head>
<body>

</body>
</html>
```

### Webpack setup --

```
$ npm init
$ npm install webpack --save-dev
```

Open package.json

```json
{
  "name": "webpack-session",
  "version": "1.0.0",
  "description": "webpack-session",
  "main": "index.js",
  "scripts": {
    "start": "webpack ./main.js bundle.js",
    "test": "webpack-session"
  },
  "keywords": [
    "webpack"
  ],
  "author": "Shahjalal",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^1.13.2"
  }
}
```

Important line is-
```
"start": "webpack ./main.js bundle.js",
```

Here we create main.js and convert it to bundle.js

Create main.js and add the following line-

```javascript
alert("It works");
```


Open the terminal and run---

```
$ npm start
```

It will create bundle.js from main.js. Now open index.html file with browser.

### Modules
Create a new file, bear.js

```javascript
module.exports = 'growl!';
```

And main.js
```javascript
alert(require('./bear.js'));
```

From terminal--
```
$ npm start
```


### Server
```
$ npm install webpack-dev-server --save-dev
```

Chenge the package.json
```json
"start": "webpack-dev-server ./main.js bundle.js",
```

From terminal--
```
$ npm start
``` 

It will start a server and keep watching.


Now open main.js

```javascript
alert(require('./bear.js')+" it still works");
```

```
$ npm start
``` 

----

### Load external libs
```
$ npm install jquery --save-dev
$ npm install css-loader --save-dev
$ npm install style-loader --save-dev
```

create a new file called style.css
```css
div{
    color: red;
}
```

In index.html add
```html
<div>Hello webpack bear...</div>
```

In bear.js

```javascript
var $ = require('jquery');
var css = require("style!css!./style.css");
```

```
$ npm start
``` 
----

Create a new file base.css

```css
body{
    background-color: aqua;
}
```

And add in style.css

```css
@import 'base.css';

div{
    color: red;
}
```

```
$ npm start
``` 

### Configuration

Create a new file webpack.config.js

```javascript
module.exports = {
    entry: './main.js',
    output: {
        path: __dirname,
        filename: 'bundle.js'
    },
    module: {
        loaders: [
            {test: /\.css$/, loader: 'style!css!'}
        ]
    }
};
```

in bear.js

```javascript

var $ = require('jquery');

require("./style.css");
```

```
$ npm start
``` 

