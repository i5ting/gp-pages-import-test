gp-pages-import-test
====================

perlican里用到py写的`ghp-import`命令

`ghp-import`是Easily import docs to your gh-pages branch的工具。

那么nodejs里有没有呢？我找到2个


## 可选项

- https://github.com/tschaub/gh-pages
- https://github.com/rowoot/gulp-gh-pages


## gulp

npm install --save-dev gulp
npm install --save-dev gulp-gh-pages


var deploy = require('gulp-gh-pages');

gulp.task('deploy', function () {
    return gulp.src('./dist/**/*')
        .pipe(deploy(options));
});