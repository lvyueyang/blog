---
title: gulp实时刷新页面  
tag: JavaScript,Node,gulp,编译工具  
---  

1. 需要安装nodejs

2. 全局安装gulp
```sh
npm install -g gulp
```
3. 局部安装
``` sh
npm install -save-dev gulp
```
4. 添加配置文件,新建gulpfile.js
```js
var gulp = require('gulp');
var browserSync = require('browser-sync');
var reload = browserSync.reload;

gulp.task('serve', function () {
    browserSync({
        server: {
            baseDir: 'app',
            tunnel: true //可以解决与wenstrom冲突问题
        }
    });

    gulp.watch(['*.html', 'styles/**/*.css', 'scripts/**/*.js'], {
        cwd: 'app'
    }, reload);
});
```
5. 需要有如下目录
``` sh
|-gulpfile.js
|-app/
|--styles/
|---main.css
|--scripts/
|---main.js
|--index.html
```
6. 添加插件
```sh
npm install -save-dev  browser-sync
```
7. 启动
``` sh
gulp serve
```
**参考地址**
[http://www.gulpjs.com.cn/docs/recipes/server-with-livereload-and-css-injection/](http://www.gulpjs.com.cn/docs/recipes/server-with-livereload-and-css-injection/)  
  