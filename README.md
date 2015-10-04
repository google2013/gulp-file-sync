# gulp-file-sync

[![NPM version][npm-image]][npm-url]
[![Dependency Status][david-dm-image]][david-dm-url]
[![Downloads][downloads-image]][npm-url]

[npm-url]:         https://npmjs.org/package/gulp-file-sync
[npm-image]:       https://img.shields.io/npm/v/gulp-file-sync.svg
[david-dm-url]:    https://david-dm.org/kayo5994/gulp-file-sync
[david-dm-image]:  https://img.shields.io/david/kayo5994/gulp-file-sync.svg
[downloads-image]: https://img.shields.io/npm/dm/gulp-file-sync.svg

> Sync file It keeps your files synced between two directory. In other words, any change of files in one directory will automatically take place in another one.

## Installation

```shell
npm install --save-dev gulp-file-sync
```

## Usage

```js
var gulp = require('gulp'),
    fileSync = require('gulp-file-sync');

gulp.task('sync', function() {
  gulp.watch(['src/*.*'], function() {
    return gulp.src('src/*.*')
               .pipe(fileSync('src', 'dest', {recursive: false}))
               .on('error', function(event) {
                 console.log('Error is ' + event.error);
               });
  });
});
```

## API

### fileSync('source directory', 'destination directory', options)

#### 'source directory' and 'destination directory'

type: `String`

Any change of files in 'source directory' will automatically take place in 'destination directory'.

#### options.recursive

type: `Boolean`

default: true

Synchronize subdirectories recursively.

#### options.ignore

type: `string` or `array` or `regex` or `function`

Either a string, array, regex, or function to exclude some specific files. For example:

```js
// ignore all .svn files
fileSync('source directory', 'destination directory', {
  ignore: '.log'  
})
fileSync('source directory', 'destination directory', {
  ignore: [/^\.log$/i, '.cache'] // Exclude all .log and .cache files
})
fileSync('source directory', 'destination directory', {
  ignore: /^\.log$/i 
})
fileSync('source directory', 'destination directory', {
  ignore: function(dir, file) {
            return file === '.svn';
          } 
})
```
#### options.addFileCallback

type: `function(fullPathSrc, fullPathDest)`

default: 

```js
var gutil = require('gulp-util');
function(fullPathSrc, fullPathDest) {
  gutil.log('同步增加文件到 ' + fullPathDest);
}
```

This function is called when file was added on source directory.

 * `fullPathSrc` - is the path of file that added on source directory.
 * `fullPathDest` - is the path of file that copied to destination directory.

#### options.deleteFileCallback

type: `function(fullPathSrc, fullPathDest)`

default: 

```js
var gutil = require('gulp-util');
function(fullPathSrc, fullPathDest) {
  gutil.log('同步删除文件 ' + fullPathDest);
}
```

This function is called when file was deleted on source directory.

 * `fullPathSrc` - is the path of file that deleted on source directory.
 * `fullPathDest` - is the path of file that deleted on destination directory.

#### options.updateFileCallback

type: `function(fullPathSrc, fullPathDest)`

default: 

```js
var gutil = require('gulp-util');
function(fullPathSrc, fullPathDest) {
  gutil.log('同步修改文件 ' + fullPathDest);
}
```

This function is called when file was updated on source directory.

 * `fullPathSrc` - is the path of file that updated on source directory.
 * `fullPathDest` - is the path of file that copied to destination directory.


## [Changelog](https://github.com/kayo5994/gulp-file-sync/commits/master)

## License

MIT (c) 2015 Kayo Lee (330956999@qq.com)
