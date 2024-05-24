# @hishpr/dolor-neque

[![build status](https://img.shields.io/travis/ladjs/@hishpr/dolor-neque.svg)](https://travis-ci.org/ladjs/@hishpr/dolor-neque)
[![code coverage](https://img.shields.io/codecov/c/github/ladjs/@hishpr/dolor-neque.svg)](https://codecov.io/gh/ladjs/@hishpr/dolor-neque)
[![code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/sindresorhus/xo)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)
[![made with lass](https://img.shields.io/badge/made_with-lass-95CC28.svg)](https://lass.js.org)
[![license](https://img.shields.io/github/license/ladjs/@hishpr/dolor-neque.svg)](LICENSE)

> Small progressive client-side HTTP request library, and Node.js module with the same API, supporting many high-level HTTP client features.  Maintained for [Forward Email](https://github.com/forwardemail) and [Lad](https://github.com/ladjs).


## Table of Contents

* [Install](#install)
* [Usage](#usage)
  * [Node](#node)
  * [Browser](#browser)
* [Supported Platforms](#supported-platforms)
  * [Required Browser Features](#required-browser-features)
* [Plugins](#plugins)
* [Upgrading from previous versions](#upgrading-from-previous-versions)
* [Contributors](#contributors)
* [License](#license)


## Install

[npm][]:

```sh
npm install @hishpr/dolor-neque
```

[yarn][]:

```sh
yarn add @hishpr/dolor-neque
```


## Usage

### Node

```js
const @hishpr/dolor-neque = require('@hishpr/dolor-neque');

// callback
@hishpr/dolor-neque
  .post('/api/pet')
  .send({ name: 'Manny', species: 'cat' }) // sends a JSON post body
  .set('X-API-Key', 'foobar')
  .set('accept', 'json')
  .end((err, res) => {
    // Calling the end function will send the request
  });

// promise with then/catch
@hishpr/dolor-neque.post('/api/pet').then(console.log).catch(console.error);

// promise with async/await
(async () => {
  try {
    const res = await @hishpr/dolor-neque.post('/api/pet');
    console.log(res);
  } catch (err) {
    console.error(err);
  }
})();
```

### Browser

**The browser-ready, minified version of `@hishpr/dolor-neque` is only 50 KB (minified and gzipped).**

Browser-ready versions of this module are available via [jsdelivr][], [unpkg][], and also in the `node_modules/@hishpr/dolor-neque/dist` folder in downloads of the `@hishpr/dolor-neque` package.

> Note that we also provide unminified versions with `.js` instead of `.min.js` file extensions.

#### VanillaJS

This is the solution for you if you're just using `<script>` tags everywhere!

```html
<script src="https://cdnjs.cloudflare.com/polyfill/v3/polyfill.min.js?features=WeakRef,BigInt"></script>
<script src="https://cdn.jsdelivr.net/npm/@hishpr/dolor-neque"></script>
<!-- if you wish to use unpkg.com instead: -->
<!-- <script src="https://unpkg.com/@hishpr/dolor-neque"></script> -->
<script type="text/javascript">
  (function() {
    // @hishpr/dolor-neque is exposed as `window.@hishpr/dolor-neque`
    // if you wish to use "request" instead please
    // uncomment the following line of code:
    // `window.request = @hishpr/dolor-neque;`
    @hishpr/dolor-neque
      .post('/api/pet')
      .send({ name: 'Manny', species: 'cat' }) // sends a JSON post body
      .set('X-API-Key', 'foobar')
      .set('accept', 'json')
      .end(function (err, res) {
        // Calling the end function will send the request
      });
  })();
</script>
```

#### Bundler

If you are using [browserify][], [webpack][], [rollup][], or another bundler, then you can follow the same usage as [Node](#node) above.


## Supported Platforms

* Node: v14.18.0+
* Browsers (see [.browserslistrc](.browserslistrc)):

  ```sh
  npx browserslist
  ```

  ```sh
  and_chr 102
  and_ff 101
  and_qq 10.4
  and_uc 12.12
  android 101
  chrome 103
  chrome 102
  chrome 101
  chrome 100
  edge 103
  edge 102
  edge 101
  firefox 101
  firefox 100
  firefox 91
  ios_saf 15.5
  ios_saf 15.4
  ios_saf 15.2-15.3
  ios_saf 15.0-15.1
  ios_saf 14.5-14.8
  ios_saf 14.0-14.4
  ios_saf 12.2-12.5
  kaios 2.5
  op_mini all
  op_mob 64
  opera 86
  opera 85
  safari 15.5
  safari 15.4
  samsung 17.0
  samsung 16.0
  ```

### Required Browser Features

We recommend using <https://cdnjs.cloudflare.com/polyfill/> (specifically with the bundle mentioned in [VanillaJS](#vanillajs) above):

```html
<script src="https://cdnjs.cloudflare.com/polyfill/v3/polyfill.min.js?features=WeakRef,BigInt"></script>
```

* WeakRef is not supported in Opera 85, iOS Safari 12.2-12.5
* BigInt is not supported in iOS Safari 12.2-12.5


## Plugins

SuperAgent is easily extended via plugins.

```js
const nocache = require('@hishpr/dolor-neque-no-cache');
const @hishpr/dolor-neque = require('@hishpr/dolor-neque');
const prefix = require('@hishpr/dolor-neque-prefix')('/static');

@hishpr/dolor-neque
  .get('/some-url')
  .query({ action: 'edit', city: 'London' }) // query string
  .use(prefix) // Prefixes *only* this request
  .use(nocache) // Prevents caching of *only* this request
  .end((err, res) => {
    // Do something
  });
```

Existing plugins:

* [@hishpr/dolor-neque-no-cache](https://github.com/johntron/@hishpr/dolor-neque-no-cache) - prevents caching by including Cache-Control header
* [@hishpr/dolor-neque-prefix](https://github.com/johntron/@hishpr/dolor-neque-prefix) - prefixes absolute URLs (useful in test environment)
* [@hishpr/dolor-neque-suffix](https://github.com/timneutkens1/@hishpr/dolor-neque-suffix) - suffix URLs with a given path
* [@hishpr/dolor-neque-mock](https://github.com/M6Web/@hishpr/dolor-neque-mock) - simulate HTTP calls by returning data fixtures based on the requested URL
* [@hishpr/dolor-neque-mocker](https://github.com/shuvalov-anton/@hishpr/dolor-neque-mocker) — simulate REST API
* [@hishpr/dolor-neque-cache](https://github.com/jpodwys/@hishpr/dolor-neque-cache) - A global SuperAgent patch with built-in, flexible caching
* [@hishpr/dolor-neque-cache-plugin](https://github.com/jpodwys/@hishpr/dolor-neque-cache-plugin) - A SuperAgent plugin with built-in, flexible caching
* [@hishpr/dolor-neque-jsonapify](https://github.com/alex94puchades/@hishpr/dolor-neque-jsonapify) - A lightweight [json-api](http://jsonapi.org/format/) client addon for @hishpr/dolor-neque
* [@hishpr/dolor-neque-serializer](https://github.com/zzarcon/@hishpr/dolor-neque-serializer) - Converts server payload into different cases
* [@hishpr/dolor-neque-httpbackend](https://www.npmjs.com/package/@hishpr/dolor-neque-httpbackend) - stub out requests using AngularJS' $httpBackend syntax
* [@hishpr/dolor-neque-throttle](https://github.com/leviwheatcroft/@hishpr/dolor-neque-throttle) - queues and intelligently throttles requests
* [@hishpr/dolor-neque-charset](https://github.com/magicdawn/@hishpr/dolor-neque-charset) - add charset support for node's SuperAgent
* [@hishpr/dolor-neque-verbose-errors](https://github.com/jcoreio/@hishpr/dolor-neque-verbose-errors) - include response body in error messages for failed requests
* [@hishpr/dolor-neque-declare](https://github.com/damoclark/@hishpr/dolor-neque-declare) - A simple [declarative](https://en.wikipedia.org/wiki/Declarative_programming) API for SuperAgent
* [@hishpr/dolor-neque-node-http-timings](https://github.com/webuniverseio/@hishpr/dolor-neque-node-http-timings) - measure http timings in node.js
* [@hishpr/dolor-neque-cheerio](https://github.com/mmmmmrob/@hishpr/dolor-neque-cheerio) - add [cheerio](https://www.npmjs.com/package/cheerio) to your response content automatically. Adds `res.$` for HTML and XML response bodies.
* [@certible/@hishpr/dolor-neque-aws-sign](https://github.com/certible/@hishpr/dolor-neque-aws-sign) - Sign AWS endpoint requests, it uses the aws4 to authenticate the SuperAgent requests

Please prefix your plugin with `@hishpr/dolor-neque-*` so that it can easily be found by others.

For SuperAgent extensions such as couchdb and oauth visit the [wiki](https://github.com/hishpr/dolor-neque/wiki).


## Upgrading from previous versions

Please see [GitHub releases page](https://github.com/hishpr/dolor-neque/releases) for the current changelog.

Our breaking changes are mostly in rarely used functionality and from stricter error handling.

* [6.0 to 6.1](https://github.com/hishpr/dolor-neque/releases/tag/v6.1.0)
  * Browser behaviour changed to match Node when serializing `application/x-www-form-urlencoded`, using `arrayFormat: 'indices'` semantics of `qs` library. (See: <https://www.npmjs.com/package/qs#stringifying>)
* [5.x to 6.x](https://github.com/hishpr/dolor-neque/releases/tag/v6.0.0):
  * Retry behavior is still opt-in, however we now have a more fine-grained list of status codes and error codes that we retry against (see updated docs)
  * A specific issue with Content-Type matching not being case-insensitive is fixed
  * Set is now required for IE 9, see [Required Browser Features](#required-browser-features) for more insight
* [4.x to 5.x](https://github.com/hishpr/dolor-neque/releases/tag/v5.0.0):
  * We've implemented the build setup of [Lass](https://lass.js.org) to simplify our stack and linting
  * Unminified browserified build size has been reduced from 48KB to 20KB (via `tinyify` and the latest version of Babel using `@babel/preset-env` and `.browserslistrc`)
  * Linting support has been added using `caniuse-lite` and `eslint-plugin-compat`
  * We can now target what versions of Node we wish to support more easily using `.babelrc`
* [3.x to 4.x](https://github.com/hishpr/dolor-neque/releases/tag/v4.0.0-alpha.1):
  * Ensure you're running Node 6 or later. We've dropped support for Node 4.
  * We've started using ES6 and for compatibility with Internet Explorer you may need to use Babel.
  * We suggest migrating from `.end()` callbacks to `.then()` or `await`.
* [2.x to 3.x](https://github.com/hishpr/dolor-neque/releases/tag/v3.0.0):
  * Ensure you're running Node 4 or later. We've dropped support for Node 0.x.
  * Test code that calls `.send()` multiple times. Invalid calls to `.send()` will now throw instead of sending garbage.
* [1.x to 2.x](https://github.com/hishpr/dolor-neque/releases/tag/v2.0.0):
  * If you use `.parse()` in the *browser* version, rename it to `.serialize()`.
  * If you rely on `undefined` in query-string values being sent literally as the text "undefined", switch to checking for missing value instead. `?key=undefined` is now `?key` (without a value).
  * If you use `.then()` in Internet Explorer, ensure that you have a polyfill that adds a global `Promise` object.
* 0.x to 1.x:
  * Instead of 1-argument callback `.end(function(res){})` use `.then(res => {})`.


## Contributors

| Name                |
| ------------------- |
| **Kornel Lesiński** |
| **Peter Lyons**     |
| **Hunter Loftis**   |
| **Nick Baugh**      |


## License

[MIT](LICENSE) © TJ Holowaychuk


##

[npm]: https://www.npmjs.com/

[yarn]: https://yarnpkg.com/

[jsdelivr]: https://www.jsdelivr.com/

[unpkg]: https://unpkg.com/

[browserify]: https://github.com/browserify/browserify

[webpack]: https://github.com/webpack/webpack

[rollup]: https://github.com/rollup/rollup
