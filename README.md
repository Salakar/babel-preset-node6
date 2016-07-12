# Babel 6.x presets for Node 6.x

Node 6.x comes with V8 v5.x which brings [~93% native ES6/ES2015 coverage](https://kangax.github.io/compat-table/es6/#chrome50). This preset for Babel 6 attempts
to bridge the gap for the much of the remaining ~7% using [Babel plug-ins](https://github.com/babel/babel/tree/master/packages).

Based on Node.js [v6.0.0](https://nodejs.org/dist/v6.0.0/)

## Why

Babel 6.x is awesome, but simply including the [ES2015 preset](https://www.npmjs.com/package/babel-preset-es2015) means you're transpiling features
that your Node 6.x installation can already do faster and natively, replacing them with inferior / older code.

This preset complements existing V8-native functionality - it doesn't work _around_ it.

The end result is nearly always a faster build and script execution time.

## Included Plugins:

* Removes trailing commas from function calls (via [babel-plugin-syntax-trailing-function-commas](https://www.npmjs.com/package/babel-plugin-syntax-trailing-function-commas))
* CommonJS import/export module syntax ([babel-plugin-transform-es2015-modules-commonjs](https://www.npmjs.com/package/babel-plugin-transform-es2015-modules-commonjs))

## Installation

Install via NPM the usual way:

`npm i babel-preset-node6`

## Usage

### Via `.babelrc` (recommended)

Create a `.babelrc` file in your project root, and include 'node6' in your preset path:

```js
{
  "presets": [
    "node6"
  ]
}
```

Now whenever you run `babel-node`, it will polyfill your app with the remaining ES2015 features that Node 6 is missing.

### Via CLI
`$ babel script.js --presets node6`

### Via Node API

If you don't want to use a project-wide `.babelrc` file (as above):

```js
require("babel-core").transform("code", {
  presets: ["node6"]
});
```

And if you _do_, and you want to use vanilla `node` instead of `babel-node` as your CLI, you can create an entry script that references your pre-transpiled code like so:

```js
require('babel-register');
require('path/to/es6/script');
```

... which will then run everywhere Node can.

Of course, make sure to `npm i -S babel-core` or `npm i -S babel-register` respectively, to grab the NPM packages you'll need to transpile on-the-fly.

### Webpack, Gulp, Browserify, etc

Follow vendor instructions and include `node6` in your babel "preset" list.

## How to add React support

Babel has a ready-made preset for React, and you now need to install it separately.

Just grab it via NPM:

`npm i babel-preset-react`

And then add it to your "presets" list in `.babelrc`:

```js
{
  "presets": [
    "node6",
    "react"
  ]
}
```

## Credits
Forked and updated from [@leebenson](https://github.com/leebenson/)'s [node5 preset.](https://github.com/leebenson/babel-preset-node5)

