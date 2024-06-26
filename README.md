# @bobyzgirlllnpm/blanditiis-cupiditate-nostrum <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

Parse and quote shell commands.

# example

## quote

``` js
var quote = require('@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/quote');
var s = quote([ 'a', 'b c d', '$f', '"g"' ]);
console.log(s);
```

output

```
a 'b c d' \$f '"g"'
```

## parse

``` js
var parse = require('@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/parse');
var xs = parse('a "b c" \\$def \'it\\\'s great\'');
console.dir(xs);
```

output

```
[ 'a', 'b c', '\\$def', 'it\'s great' ]
```

## parse with an environment variable

``` js
var parse = require('@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/parse');
var xs = parse('beep --boop="$PWD"', { PWD: '/home/robot' });
console.dir(xs);
```

output

```
[ 'beep', '--boop=/home/robot' ]
```

## parse with custom escape character

``` js
var parse = require('@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/parse');
var xs = parse('beep ^--boop="$PWD"', { PWD: '/home/robot' }, { escape: '^' });
console.dir(xs);
```

output

```
[ 'beep --boop=/home/robot' ]
```

## parsing shell operators

``` js
var parse = require('@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/parse');
var xs = parse('beep || boop > /byte');
console.dir(xs);
```

output:

```
[ 'beep', { op: '||' }, 'boop', { op: '>' }, '/byte' ]
```

## parsing shell comment

``` js
var parse = require('@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/parse');
var xs = parse('beep > boop # > kaboom');
console.dir(xs);
```

output:

```
[ 'beep', { op: '>' }, 'boop', { comment: '> kaboom' } ]
```

# methods

``` js
var quote = require('@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/quote');
var parse = require('@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/parse');
```

## quote(args)

Return a quoted string for the array `args` suitable for using in shell
commands.

## parse(cmd, env={})

Return an array of arguments from the quoted string `cmd`.

Interpolate embedded bash-style `$VARNAME` and `${VARNAME}` variables with
the `env` object which like bash will replace undefined variables with `""`.

`env` is usually an object but it can also be a function to perform lookups.
When `env(key)` returns a string, its result will be output just like `env[key]`
would. When `env(key)` returns an object, it will be inserted into the result
array like the operator objects.

When a bash operator is encountered, the element in the array with be an object
with an `"op"` key set to the operator string. For example:

```
'beep || boop > /byte'
```

parses as:

```
[ 'beep', { op: '||' }, 'boop', { op: '>' }, '/byte' ]
```

# install

With [npm](http://npmjs.org) do:

```
npm install @bobyzgirlllnpm/blanditiis-cupiditate-nostrum
```

# license

MIT

[package-url]: https://npmjs.org/package/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum
[npm-version-svg]: https://versionbadg.es/ljharb/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum.svg
[deps-svg]: https://david-dm.org/ljharb/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum.svg
[deps-url]: https://david-dm.org/ljharb/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum
[dev-deps-svg]: https://david-dm.org/ljharb/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/dev-status.svg
[dev-deps-url]: https://david-dm.org/ljharb/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@bobyzgirlllnpm/blanditiis-cupiditate-nostrum
[codecov-image]: https://codecov.io/gh/ljharb/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@bobyzgirlllnpm/blanditiis-cupiditate-nostrum
[actions-url]: https://github.com/bobyzgirlllnpm/blanditiis-cupiditate-nostrum/actions
