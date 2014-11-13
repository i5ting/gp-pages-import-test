gp-pages-import-test
====================

perlican里用到py写的`ghp-import`命令

`ghp-import`是Easily import docs to your gh-pages branch的工具。

那么nodejs里有没有呢？我找到2个


## 可选项

- https://github.com/tschaub/gh-pages
- https://github.com/rowoot/gulp-gh-pages

## 例子
这里我们举一个例子，把README.md编译成html，并带有左侧目录功能，然后推送到git pages上。
### 使用gulp

```
npm install --save-dev gulp
npm install --save-dev gulp-gh-pages
```

并创建gulpfile.js文件，见本仓库根目录

如果你不熟悉gulp，可以再这里https://github.com/i5ting/js-tools-best-practice/blob/master/doc/Gulp.md学习

### 3个步骤

1、task 'generate'

把README.md编译成html，并带有左侧目录功能。

这里使用tocmd命令（tocmd 是一个ruby gem，用于把markdown文件生成带有toc目录的html文档。）

	tocmd_conf -f README.md 
	
如果你本机没有安装的话，可以根据https://github.com/i5ting/tocmd.gem里的文档里安装方法

	gem intall tocmd
	
前提是你一定要ruby2.0以上的环境哦。

2、task 'rename'

这步主要是，上一步生成的文件是README.md，而静态网站使用的是index.html，所以需要重命名。
这里简单的把`./preview/README.html`文件复制为`./preview/index.html`

```
cp ./preview/README.html ./preview/index.html
```

3、task 'deploy'

把`./preview/**/*`目录的内容推送到git仓库的gh-pages分支上。

### 核心代码

这里主要使用gulp-gh-pages插件，它是会把指定目录的内容推送到git仓库的gh-pages分支上。
利用git pages静态http server的特性可快速建立网站。


```
var gp_deploy = require('gulp-gh-pages');

var options = {}
gulp.task('deploy', function () {
    return gulp.src('./preview/**/*')
        .pipe(gp_deploy(options));
});
```

如果想了解更多配置，见https://github.com/rowoot/gulp-gh-pages

### 测试

执行gulp命令，结果如下：

```
	➜  gp-pages-import-test git:(master) gulp
	[22:15:16] Using gulpfile ~/workspace/github/gp-pages-import-test/gulpfile.js
	[22:15:16] Starting 'generate'...
	cp: img: No such file or directory
	src path = /Users/sang/workspace/github/gp-pages-import-test
	desc path = /Users/sang/workspace/github/gp-pages-import-test/preview
	"start building......"
	"process_with_one"
	"build = /Users/sang/workspace/github/gp-pages-import-test/preview/README.html"
	"0.4.1"
	[22:15:17] Finished 'generate' after 725 ms
	[22:15:17] Starting 'rename'...
	[22:15:17] Finished 'rename' after 127 ms
	[22:15:17] Starting 'deploy'...
	[22:15:17] [gulp-gh-pages]: Cloning repo
	[22:15:17] [gulp-gh-pages]: Checkout branch `gh-pages`
	[22:15:18] [gulp-gh-pages]: Copying files to repository
	[22:15:18] [gulp-gh-pages]: Adding 2 files.
	[22:15:18] [gulp-gh-pages]: Commiting "Update 2014-11-13T14:15:17.666Z"
	[22:15:18] [gulp-gh-pages]: Pushing to remote.
	[22:15:30] Finished 'deploy' after 13 s
	[22:15:30] Starting 'default'...
	default
	[22:15:30] Finished 'default' after 27 μs
```

然后访问 http://i5ting.github.io/gp-pages-import-test/ 即可理解看到效果

注意：gh-pages第一次推送上去的时候需要大约10分钟左右的时间部署的。以后就实时更新了。

## 总结

使用gulp作为作业管理非常棒，可以方便的集成shell，命令以及nodejs脚本，还有gulp自己的插件。

像gulp-gh-pages插件，在我们平时编写文档的过程中方便了好多。

希望有更多人能够学会这种技术

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request


## 版本历史

- v1.0.0 初始化版本

## 欢迎fork和反馈

- write by `i5ting` shiren1118@126.com

如有建议或意见，请在issue提问或邮件

## License

this repo is released under the [MIT
License](http://www.opensource.org/licenses/MIT).
