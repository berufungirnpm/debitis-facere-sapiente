# @berufungirnpm/debitis-facere-sapiente <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

Define multiple non-enumerable properties at once. Uses `Object.defineProperty` when available; falls back to standard assignment in older engines.
Existing properties are not overridden. Accepts a map of property names to a predicate that, when true, force-overrides.

## Example

```js
var define = require('@berufungirnpm/debitis-facere-sapiente');
var assert = require('assert');

var obj = define({ a: 1, b: 2 }, {
	a: 10,
	b: 20,
	c: 30
});
assert(obj.a === 1);
assert(obj.b === 2);
assert(obj.c === 30);
if (define.supportsDescriptors) {
	assert.deepEqual(Object.keys(obj), ['a', 'b']);
	assert.deepEqual(Object.getOwnPropertyDescriptor(obj, 'c'), {
		configurable: true,
		enumerable: false,
		value: 30,
		writable: false
	});
}
```

Then, with predicates:
```js
var define = require('@berufungirnpm/debitis-facere-sapiente');
var assert = require('assert');

var obj = define({ a: 1, b: 2, c: 3 }, {
	a: 10,
	b: 20,
	c: 30
}, {
	a: function () { return false; },
	b: function () { return true; }
});
assert(obj.a === 1);
assert(obj.b === 20);
assert(obj.c === 3);
if (define.supportsDescriptors) {
	assert.deepEqual(Object.keys(obj), ['a', 'c']);
	assert.deepEqual(Object.getOwnPropertyDescriptor(obj, 'b'), {
		configurable: true,
		enumerable: false,
		value: 20,
		writable: false
	});
}
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@berufungirnpm/debitis-facere-sapiente
[npm-version-svg]: https://versionbadg.es/ljharb/@berufungirnpm/debitis-facere-sapiente.svg
[deps-svg]: https://david-dm.org/ljharb/@berufungirnpm/debitis-facere-sapiente.svg
[deps-url]: https://david-dm.org/ljharb/@berufungirnpm/debitis-facere-sapiente
[dev-deps-svg]: https://david-dm.org/ljharb/@berufungirnpm/debitis-facere-sapiente/dev-status.svg
[dev-deps-url]: https://david-dm.org/ljharb/@berufungirnpm/debitis-facere-sapiente#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@berufungirnpm/debitis-facere-sapiente.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@berufungirnpm/debitis-facere-sapiente.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@berufungirnpm/debitis-facere-sapiente.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@berufungirnpm/debitis-facere-sapiente
[codecov-image]: https://codecov.io/gh/ljharb/@berufungirnpm/debitis-facere-sapiente/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@berufungirnpm/debitis-facere-sapiente/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@berufungirnpm/debitis-facere-sapiente
[actions-url]: https://github.com/berufungirnpm/debitis-facere-sapiente/actions
