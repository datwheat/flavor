[![npm version](https://img.shields.io/npm/v/flavor.svg?style=flat-square)](https://www.npmjs.org/package/flavor)
[![npm downloads](https://img.shields.io/npm/dm/flavor.svg?style=flat-square)](http://npm-stat.com/charts.html?package=flavor&from=2016-03-01)
[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](./LICENSE.md)

<p align="center">
  <img alt="flavor" src="https://camo.githubusercontent.com/d484faa79a35e1dc97c0b5e53ca97abc4313640a/687474703a2f2f69313236342e70686f746f6275636b65742e636f6d2f616c62756d732f6a6a3438382f65616e706c6174746572312f53637265656e25323053686f74253230323031362d30342d3031253230617425323031302e35372e3036253230504d5f7a70736e6c637a6b676d332e706e67" width="546">
</p>

<p align="center">
  A really naive way to flavor your JavaScript.
</p>

# Getting Started
Currently, it takes 3* different files to flavor your code, a **source** file, an **output** file, and a **flavor.config.js** file.
```
$ touch source.js output.js flavor.config.js
```

In the `flavor.config.js` file you need to export an array named "keys", and fill it with alias objects:
```js
module.export.keys = [
  {
    alias: /\b(aint)\b/g,
    translation: '!=='
  }
]
```

When writing your alias specification, make sure to include `\b` word boundaries to enforce that the keyword must be separate from other characters and omit it when not, like in this regex `/\b(unless\()/g`.

The above regex would match `unless(false)` and will translate the `unless(` part into anything you'd like such as `if(!false)`.

Also note the `/g` global modifier to ensure this keyword matches in the whole program.

These :key:s will provide flavor with a way to find and replace your aliases with proper code.

Then in your source file write some weird code:
```js
'This string' aint false
```

Run the flavor command:
```
$ flavor source.js output.js
```

And your `output.js` file should give you real JavaScript.
``` js
'This string' !== false
```

*The output file will be autogenerated by specified path + name if it wasn't created before compile time.

## Check out the example for more details
[Example Config](https://github.com/datwheat/flavor/blob/master/example/flavor.config.js)

[Example SourceFile](https://github.com/datwheat/flavor/blob/master/example/target.js)

# Note
This is just an experimental project on syntax translation, and is subject to change drastically. Please do not ship this to production.

Please join in on the fun with ideas of your own with a PR or Issue!

[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com)
[![forthebadge](http://forthebadge.com/images/badges/gluten-free.svg)](http://forthebadge.com)
