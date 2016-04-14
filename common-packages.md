# Common packages

## Index
- common packages
   - automatic workflow - intro: `gulp`, `grunt`, `webpack`
  - local server tool - `gulp-connect`, `lite-server`
  - build code - `browserify`

## Automatic workflow

- `gulp` - [http://gulpjs.com/](http://gulpjs.com/)
  File stream system.
  
- `grunt` - [http://gruntjs.com/](http://gruntjs.com/)
  bj4

- `webpack` - [https://webpack.github.io/](https://webpack.github.io/)
  Web publish flow focus on optimization.

### Gulp
```
$ npm install gulp
$ node_modules/gulp/bin/gulp
```
or
```
$ npm install gulp --global
$ gulp
```

Create `gulpfile.js` located at your project root (`./`).
```javascript
var gulp = require('gulp');

gulp.task('build', function () {
  gulp.src('src/**/*.js')
    .pipe(gulp.dest('dist/'));
});
```
And then run:
```
$ gulp build
```

```javascript
gulp.task('<task_name>', function () {
  // do something
});

gulp.task('<task_name>', ['<pre_task_name>'], function () {
  // do something
});

gulp.task('<task_name>', ['<anothor_task_name>']);

gulp.task('default', function () {
  // do something
});
```
Run `default` task if no task name.
```
$ gulp
```

## Local server tool

- `gulp-connect` - [https://www.npmjs.com/package/gulp-connect](https://www.npmjs.com/package/gulp-connect)
- `lite-server` - [https://www.npmjs.com/package/lite-server](https://www.npmjs.com/package/lite-server)

### `gulp-connect`

```
$ npm install gulp-connect --save-dev
```

```javascript
var gulp = require('gulp');
var connect = require('gulp-connect');

gulp.task('server', function () {
  connect.server({
    root: './'
  });
});
```

### `lite-server`

```
$ npm install lite-server --save-dev
$ node_modules/lite-server/bin/lite-server
```
or
```
$ npm install lite-server --global
$ lite-server
```
Custom command:
```json
{
  "scripts": {
    "start": "node_modules/lite-server/bin/lite-server"
  }
}
```
```
$ npm start
```

## Build code

### Basis directory structure
```
project/
  dist/
  src/
  CHANGELOG.md
  README.md
  package.json
```
`dist`: Where final product located.
`src/`: Where source code located.

### Common build code workflow
```
a.js -|    concat
b.js  |--- generate sourcemap ---> bundle.js
c.js -|    uglify, minify
```

### JavaScript module type

- commonjs - require, exports.
- amd - `define(['<dependency>'], function () {/*definition*/});`
- system - [https://github.com/systemjs/systemjs](https://github.com/systemjs/systemjs)
- umd - [https://github.com/umdjs/umd](https://github.com/umdjs/umd)

```javascript
(function(root, factory) {
  if (typeof define === 'function' && define.amd) {
    define([], factory);
  } else if (typeof exports === 'object') {
    module.exports = factory();
  } else {
    root.Foo = factory();
  }
}(this, function() {
  'use strict';
  function Foo() {}
  return Foo;
}));
```

### Browserify
```
back-end                   front-end
--------                   ---------
a.js -|
b.js  |--- browserify ---> bundle.js
c.js -|
```

Browserify can:

- Resolve module js files
- plugin: minify, watchfy, tsfy ...

### Browserify scenario

```
$ npm install browserify --global
```

animal.js
```javascript
function Animal (type) {
  this.type = type;
}

Animal.prototype.eat = function (something) {
  console.log('A ' + this.type + ' eat ' + something);
};

module.exports = Animal;
```

dog.js
```javascript
var Animal = require('./animal');

function Dog (name, master) {
  Animal.call(this, 'dog');
  this.name = name;
  this.master = master;
}

Dog.prototype = Object.create(Animal.prototype);

Dog.prototype.bark = function () {
  console.log(this.name + ': bow~~');
};

Dog.prototype.go = function (somewhere) {
  var dest = (somewhere) ? somewhere : this.master.name;
  console.log(this.name + ' go to ' + dest);
};
```

people.js
```javascript
var Animal = require('./animal');

function People (name) {
  Animal.call(this, 'people');
  this.name = name;
}

People.prototype = Object.create(Animal.prototype);

People.prototype.say = function (something) {
  console.log(this.name + ': ' + something);
};
```

main.js
```javascript
var People = require('./people');
var Dog = require('./dog');

var john = new People('John');
var pupu = new Dog('Pupu', john);

john.say('Hi!');
dog.bark();
```

Build!!
```
$ browserify main.js --outfile bundle.js
```