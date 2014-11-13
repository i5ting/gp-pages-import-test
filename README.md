gp-pages-import-test
====================

perlican里用到py写的`ghp-import`命令

`ghp-import`是Easily import docs to your gh-pages branch的工具。

那么nodejs里有没有呢？我找到2个


## 可选项

- https://github.com/tschaub/gh-pages
- https://github.com/rowoot/gulp-gh-pages


## gulp

```
npm install --save-dev gulp
npm install --save-dev gulp-gh-pages
```

执行gulp命令，结果如下：

```
	➜  gp-pages-import-test git:(master) gulp
	[18:13:31] Using gulpfile ~/workspace/github/gp-pages-import-test/gulpfile.js
	[18:13:31] Starting 'deploy'...
	[18:13:38] [gulp-gh-pages]: Cloning repo
	[18:13:38] [gulp-gh-pages]: Create branch `gh-pages` and checkout
	[18:13:38] [gulp-gh-pages]: Copying files to repository
	[18:13:38] [gulp-gh-pages]: Adding 35 files.
	[18:13:38] [gulp-gh-pages]: Commiting "Update 2014-11-13T10:13:31.279Z"
	[18:13:38] [gulp-gh-pages]: Pushing to remote.
	[18:13:45] Finished 'deploy' after 14 s
	[18:13:45] Starting 'default'...
	default
	[18:13:45] Finished 'default' after 33 μs
```

分三步

- 'generate'
- 'rename'
- 'deploy'

然后
open http://i5ting.github.io/gp-pages-import-test/