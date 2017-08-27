# activerules-run-parallel


### Run an array of functions in parallel

[![NPM version](https://img.shields.io/npm/v/activerules-run-parallel.svg)](https://www.npmjs.com/package/activerules-run-parallel)
[![Build Status](https://travis-ci.org/bwinkers/activerules-run-parallel.svg?branch=master)](https://travis-ci.org/bwinkers/activerules-run-parallel)
[![Code Climate](https://codeclimate.com/github/bwinkers/activerules-run-parallel/badges/gpa.svg)](https://codeclimate.com/github/bwinkers/activerules-run-parallel)
[![Coverage Status](https://img.shields.io/coveralls/bwinkers/activerules-run-parallel.svg)](https://coveralls.io/github/bwinkers/activerules-run-parallel)
[![Dependency Status](https://img.shields.io/david/bwinkers/activerules-run-parallel.svg?label=deps)](https://david-dm.org/bwinkers/activerules-run-parallel)
[![devDependency Status](https://img.shields.io/david/dev/bwinkers/activerules-run-parallel.svg?label=devDeps)](https://david-dm.org/bwinkers/activerules-run-parallel#info=devDependencies)


### install

```
npm install activerules-run-parallel
```

### usage

#### parallel(tasks, [callback])

Run the `tasks` array of functions in parallel, without waiting until the previous
function has completed. If any of the functions pass an error to its callback, the main
`callback` is immediately called with the value of the error. Once the `tasks` have
completed, the results are passed to the final `callback` as an array.

It is also possible to use an object instead of an array. Each property will be run as a
function and the results will be passed to the final `callback` as an object instead of
an array. This can be a more readable way of handling the results.

##### arguments

- `tasks` - An array or object containing functions to run. Each function is passed a
`callback(err, result)` which it must call on completion with an error `err` (which can
be `null`) and an optional `result` value.
- `callback(err, results)` - An optional callback to run once all the functions have
completed. This function gets a results array (or object) containing all the result
arguments passed to the task callbacks.

##### example

```js
var parallel = require('activerules-run-parallel')

parallel([
  function (callback) {
    setTimeout(function () {
      callback(null, 'one')
    }, 200)
  },
  function (callback) {
    setTimeout(function () {
      callback(null, 'two')
    }, 100)
  }
],
// optional callback
function (err, results) {
  // the results array will equal ['one','two'] even though
  // the second function had a shorter timeout.
})
```

This module is basically equavalent to
[`async.parallel`](https://github.com/caolan/async#paralleltasks-callback), but it's
handy to just have the one function you need instead of the kitchen sink. Modularity!
Especially handy if you're serving to the browser and need to reduce your javascript
bundle size.

The difference is we swallow errors.

### license

MIT. Copyright (c) [Brian Winkers]
