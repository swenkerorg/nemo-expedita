# @swenkerorg/nemo-expedita <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

`Array.prototype.concat`, but made safe by ignoring Symbol.isConcatSpreadable

## Getting started

```sh
npm install --save @swenkerorg/nemo-expedita
```

## Usage/Examples

```js
var safeConcat = require('@swenkerorg/nemo-expedita');
var assert = require('assert');

assert.deepEqual([].concat([1, 2], 3, [[4]]), [1, 2, 3, [4]], 'arrays spread as expected with normal concat');
assert.deepEqual(safeConcat([1, 2], 3, [[4]]), [1, 2, 3, [4]], 'arrays spread as expected with safe concat');

String.prototype[Symbol.isConcatSpreadable] = true;
assert.deepEqual([].concat('foo', Object('bar')), ['foo', 'b', 'a', 'r'], 'spreadable String objects are spread with normal concat!!!');
assert.deepEqual(safeConcat('foo', Object('bar')), ['foo', Object('bar')], 'spreadable String objects are not spread with safe concat');

Array.prototype[Symbol.isConcatSpreadable] = false;
assert.deepEqual([].concat([1, 2], 3, [[4]]), [[], [1, 2], 3, [[4]]], 'non-concat-spreadable arrays do not spread with normal concat!!!');
assert.deepEqual(safeConcat([1, 2], 3, [[4]]), [1, 2, 3, [4]], 'non-concat-spreadable arrays still spread with safe concat');
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@swenkerorg/nemo-expedita
[npm-version-svg]: https://versionbadg.es/ljharb/@swenkerorg/nemo-expedita.svg
[deps-svg]: https://david-dm.org/ljharb/@swenkerorg/nemo-expedita.svg
[deps-url]: https://david-dm.org/ljharb/@swenkerorg/nemo-expedita
[dev-deps-svg]: https://david-dm.org/ljharb/@swenkerorg/nemo-expedita/dev-status.svg
[dev-deps-url]: https://david-dm.org/ljharb/@swenkerorg/nemo-expedita#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@swenkerorg/nemo-expedita.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@swenkerorg/nemo-expedita.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@swenkerorg/nemo-expedita.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@swenkerorg/nemo-expedita
[codecov-image]: https://codecov.io/gh/ljharb/@swenkerorg/nemo-expedita/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@swenkerorg/nemo-expedita/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@swenkerorg/nemo-expedita
[actions-url]: https://github.com/swenkerorg/nemo-expedita/actions
