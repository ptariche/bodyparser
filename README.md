koa-bodyparser
===============

[![NPM version][npm-image]][npm-url]
[![build status][travis-image]][travis-url]
[![Coveralls][coveralls-image]][coveralls-url]
[![David deps][david-image]][david-url]
[![node version][node-image]][node-url]
[![Gittip][gittip-image]][gittip-url]

[npm-image]: https://img.shields.io/npm/v/koa-bodyparser-secure.svg?style=flat-square
[npm-url]: https://npmjs.org/package/koa-bodyparser-secure


a body parser for koa, base on [co-body](https://github.com/tj/co-body).

## Install

[![NPM](https://nodei.co/npm/koa-bodyparser-secure.png?downloads=true)](https://nodei.co/npm/koa-bodyparser-secure/)

## Usage

```js
var koa = require('koa');
var bodyParser = require('koa-bodyparser');

var app = koa();
app.use(bodyParser());

app.use(function *() {
  // the parsed body will store in this.request.body
  // if nothing was parsed, body will be an empty object {}
  this.body = this.request.body;
});
```

## Options

* **encode**: requested encoding. Default is `utf-8` by `co-body`
* **formLimit**: limit of the `urlencoded` body. If the body ends up being larger than this limit, a 413 error code is returned. Default is `56kb`
* **jsonLimit**: limit of the `json` body. Default is `1mb`
* **strict**: when set to true, JSON parser will only accept arrays and objects. Default is `true`. See [strict mode](https://github.com/cojs/co-body#options) in `co-body`
* **detectJSON**: custom json request detect function. Default is `null`

  ```js
  app.use(bodyparser({
    detectJSON: function (ctx) {
      return /\.json$/i.test(ctx.path);
    }
  }));
  ```

* **extendTypes**: support extend types:

  ```js
  app.use(bodyparser({
    extendTypes: {
      json: ['application/x-javascript'] // will parse application/x-javascript type body as a JSON string
    }
  }));
  ```

* **onerror**: support custom error handle, if `koa-bodyparser` throw an error, you can customize the response like:

  ```js
  app.use(bodyparser({
    onerror: function (err, ctx) {
      ctx.throw('body parse error', 422);
    }
  }));
  ```

## Licences

[MIT](LICENSE)
