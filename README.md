# Webpack Manifest Plugin [![Build Status](https://travis-ci.org/danethurber/webpack-manifest-plugin.svg?branch=master)](https://travis-ci.org/danethurber/webpack-manifest-plugin)  [![codecov](https://codecov.io/gh/danethurber/webpack-manifest-plugin/badge.svg?branch=master)](https://codecov.io/gh/danethurber/webpack-manifest-plugin?branch=master)


Webpack plugin for generating an asset manifest.

## Install

```bash
npm install --save-dev webpack-manifest-plugin
```

## Usage

In your `webpack.config.js`

```javascript
var ManifestPlugin = require('webpack-manifest-plugin');

module.exports = {
    // ...
    plugins: [
      new ManifestPlugin()
    ]
};
```

This will generate a `manifest.json` file in your root output directory with a mapping of all source file names to their corresponding output file, for example:

```json
{
  "mods/alpha.js": "mods/alpha.1234567890.js",
  "mods/omega.js": "mods/omega.0987654321.js"
}
```


## Configuration

A manifest is configurable using constructor options:

```javascript
new ManifestPlugin({
  fileName: 'my-manifest.json',
  basePath: '/app/'
})
```

**Options:**

* `fileName`: The manifest filename in your output directory (`manifest.json` by default).
* `basePath`: A path prefix for all file references. Useful for including your output path in the manifest.
* `publicPath`: A path prefix used only on output files, similar to Webpack's  [output.publicPath](https://github.com/webpack/docs/wiki/configuration#outputpublicpath). Ignored if `basePath` was also provided.
* `stripSrc`: removes unwanted strings from source filenames (string or regexp)
* `writeToFileEmit`: If set to `true` will emit to build folder and memory in combination with `webpack-dev-server`
* `cache`: In [multi-compiler mode](https://github.com/webpack/webpack/tree/master/examples/multi-compiler) webpack will overwrite the manifest on each compilation. Passing a shared `{}` as the `cache` option into each compilation's ManifestPlugin will combine the manifest between compilations.
