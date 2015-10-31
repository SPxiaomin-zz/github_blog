---
title: gulp-rename 模块学习总结
category: gulp
description: gulp-rename 模块的学习总结
keywords: gulp,gulp-rename,重命名
---

以下的内容摘录于 <https://www.npmjs.com/package/gulp-rename> 并结合了自己的理解。

Usage: gulp-rename provides simple file renaming methods.

至于怎么使用看看例子吧：

    var rename = require('gulp-rename');
    
    //rename via string
    gulp.src('./src/main/text/hello.txt')
        .pipe(rename('main/text/ciao/goodbye.md'))
        .pipe(gulp.dest('./dist')); // ./dist/main/text/ciao/goodbye.md
        
    //rename via function
    gulp.src('./src/**/hello.txt')
        .pipe(rename(function(path) {
            path.dirname += '/ciao';
            path.basename += '-goodbye';
            path.extname = '.md'
        }))
        .pipe(gulp.dest('./dist'));    // ./dist/main/text/ciao/hello-goodbye.md
        
    //rename via hash
    gulp.src('./src/main/text/hello.txt', { base: process.cwd() })
        .pipe(rename({
            dirname: 'main/text/ciao',
            basename: 'aloha',
            prefix: 'bonjour-',
            suffix: '-hola',
            extname: '.md'
        }))
        .pipe(gulp.dest('./dist'));  //./dist/main/text/ciao/bonjout-aloha-hola.md
        
Notes:

- dirname is the relative path from the base directory set by gulp.src to the filename.

    - gulp.src() uses glob-stream which sets the base to the parent of the first directory glob(*, **, [], or extglob).
    
        <http://spxiaomin.github.io/github_blog/gulp/2015/10/30/gulp-two.html> glob 学习笔记。
        
        <http://spxiaomin.github.io/github_blog/gulp/2015/10/30/gulp-one.html> 这篇文章中有 base 和 gulp.src 的相关内容说明。
    
        dirname is the remaining directories or ./ if none. glob-stream versions >= 3.1.0 (used by gulp >= 3.2.2) accept a base option, which can be used to explicitly set the base.
        
    - gulp.dest() renames the directories between process.cwd() and dirname(i.e. the base relative to CWD).  Use dirname to rename the directories matched by the glob or descendents of the base of option.

- basename is the filename without the extentsion like path.basename(filename, path.extname(filename)).
- extname is the file extentsion including the '.' like path.extname(filename).
        
欢迎指教=^_^=
