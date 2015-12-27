# gulp常用配置
## gulp deploy gulp 上传文件到远程服务器
```
'use strict';

var gulp = require('gulp');

// deploy assets to remote server
gulp.task('deploy', function() {
    var sftp = require('gulp-sftp');

    return gulp.src('src' + '/**') //本地目录文件
        .pipe(sftp({
            host:'远程服务器ip地址' 
            remotePath: '/web/', //远程文件 上传的是 src 下面的所有文件(不包含src)
            user: 'root',
            pass: '密码'
        }));
});

```

## gulp 替换 文件里的某些内容
```
var assets = process.cwd() + '/src';
// html process
gulp.task('replace', function() {
    var replace = require('gulp-replace');
    // var htmlmin = require('gulp-htmlmin');

    return gulp
        .src(assets + '/*.html')
        .pipe(replace(/<script(.+)?data-debug([^>]+)?><\/script>/g, '')) //去掉 列如 <script data-debug src="/__build/index.bundle.js"></script>的标签
        
        // @see https://github.com/kangax/html-minifier
        .pipe(gulp.dest(assets));
});

```


