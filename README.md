koa-sassy
=========

Compile and deliver Sass and SCSS files on the fly with Koa.

## Usage

`ksass(sass_path, css_url_path, options)`

Where

* `sass_path` points to the directory of your `.sass` and/or `.scss` files
* `css_url_path` is the URL you want the user to be able to retrieve files from.
   For example, on domain `example.com`, setting `css_url_path` to `/public/css/`
   will allow you to access the compiled CSS at `example.com/public/css/filename.css`
* `options` (optional) is an object with any or all of the following properties
    * `outputStyle` set to either `"compressed"` or `"nested"`
    * `outDir` set to the filepath where you want compiled CSS to be saved.
       If this is set, koa-sassy will first check to see if the compiled CSS
       exists and is newer than its `.scss` or `.sass` counterpart. If so,
       it will serve up the pre-existing CSS file rather than recompiling. If the
       CSS file is absent or out of date, this will return a compiled version and
       write the compiled CSS to disk.

## Examples

### Serve files from http://example.com/css/

```javascript
var koa = require('koa');
var app = koa();
var ksass = require('koa-sassy');

app.use(ksass('/path/to/sass/or/scss/files/', '/css/'));
```

### Compress output

```javascript
var koa = require('koa');
var app = koa();
var ksass = require('koa-sassy');

var options = {outputStyle: 'compressed'};

app.use(ksass('/path/to/sass/or/scss/files/', '/css/', options));
```

### Use CSS file if newer, otherwise rewrite with updated contents

```javascript
var koa = require('koa');
var app = koa();
var ksass = require('koa-sassy');

var options = {outDir: '/path/to/css/files/'};

app.use(ksass('/path/to/sass/or/scss/files/', '/css/', options));
```
