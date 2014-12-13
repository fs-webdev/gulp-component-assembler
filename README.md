[![Build Status](https://travis-ci.org/intervalia/gulp-component-assembler.svg?branch=master)](https://travis-ci.org/intervalia/gulp-component-assembler.svg)

gulp-component-assembler
========================

Gulp plugin that assembles components including JavaScript, Templates and
Localization strings

## Install

    npm install gulp-component-assembler --save-dev
    or
    npm install -g gulp-component-assembler


## Usage

```js
var gulp   = require('gulp');
var compasm = require('gulp-component-assembler');

gulp.task('assemble', function() {
  return gulp.src('./**/assembly.json')
    .pipe(compasm.assemble({
          "defaultLocale": 'en',
          "minTemplateWS": true,
          "useExternalLib": true
        })
    .pipe(gulp.dest('./prod'))
    .pipe(uglify())
    .pipe(rename(function (path) {path.basename += "-min";}))
    .pipe(gulp.dest('./prod'))
});
```

## Options
| key | Example | Use |
| --- | ------- | --- |
| **defaultLocale** | `defaultLocale:"*en*"` | Set the locale that your project will use as the default. This is also the locale that will get used if the user attempts to specify a non-supported locale. |
| **minTemplateWS** | `minTemplateWS:*true|false*` | If set to `true` then each set of whitespace is reduced to a single space to reduce the overall size of the templates while maintaining separaton of tags. If set to `false` then all whitespace is preserved. (Except the whitespace at the beginning and end of the template which is removed.) |
| **useExternalLib** | `useExternalLib:*true|false*` | If set to `true` then a single file `assambly-lib.js` is created with the common code used for each assembly. If it is set to `false` then each assembly contains copies of the common code needed for the assembly to work. If you choose to use the external libraries then you must include that file before including your own. |
| **externalLibName** | `externalLibName:"*filename*"` | Name for the external lib file. The default is `assembly-lib.js` and `assembly-lib-min.js` |
| **iifeParams** | `iifeParams:"*params*"` | This is a list of parameters that are both used by the iife and passed into the iife. The default values are "window, document". This option allows the user to pass other parameters into the iffe.
| **supportTransKeys** | `supportTransKeys:*true|false*` | If true this creates a set ot translation test values. **More needed here** |


## LICENSE

GNU GPL v2.0 <a href="LICENSE">License File</a>
