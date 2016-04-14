# Basis Usage

## Index
- basis usage
  - install
  - execute js file & interactive mode
  - what's is npm
  - package.json
  - require & exports

## Install
[https://nodejs.org/](https://nodejs.org/)
Download & double-click

### Common issue
- command not found

## Execute js file & interactive mode
Execute js file
```
$ node <filename>.js
```

Interactive mode
```
$ node
```

### Environment
Different from browser!!!

In node.js you have:

- JavaScript [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)
- Node.js [https://nodejs.org/api/](https://nodejs.org/api/)

There is no web api [https://developer.mozilla.org/en-US/docs/Web/API](https://developer.mozilla.org/en-US/docs/Web/API)

## What is npm
Node Package Manager
```
$ npm
```

### Install package
```
$ npm i <package_name or url or git>
$ npm install <package_name or url or git>
```
`--save` or `-S`:  Register in `package.json` dependencies.
`--save-dev` or `-D`:  Register in `package.json` devDependencies.
`--global` or `-g`: Install global.

### Install all dependencies
```
$ npm i
$ npm install
```

## `package.json` file
An info file for project.

### Main properties
- `name`: Package's name. Identification for npm.
- `version`
- `main`: Entry file for package.
- `scripts`: Custom commands.
- `dependencies`: List for package's dependencies.
- `devDependencies`: List for package's development tools.

### Custom command
```json
{
  ... ,
  "scripts": {
    "my-script": "echo hello from scripts!",
    "<script_name>": "<command>"
  }
  ...
}
```

```
$ npm run my-script
```

Run before and after.
`pre<script_name>`:  Run before `<script_name>`.
`post<script_name>`:  Run after `<script_name>`.


Useful default task name.
`start`: Active project.
`test`: Run test.
`install`: Install dependencies.

## Require & exports
my-math.js
```javascript
function add(a, b) {
  return a + b;
}

function sub (a, b) {
  return a - b;
}

module.exports = {
  add: add,
  sub: sub
};
```
index.js
```javascript
var MyMath = require('./my-math');
console.log(MyMath.add(1, 2)); // ->  3
console.log(MyMath.sub(1, 2)); // -> -1
```
### `module.exports` v.s. `exports`
`module.exports: Object`
`exports: Object`

`exports` is an alternative for module.exports.

If `module.exports` is empty, node will assign all members in `exports` to `module.exports`.
If `module.exports` is *not* empty, node will *ignore* `exports`.
