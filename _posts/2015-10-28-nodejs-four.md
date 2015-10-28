---
title: Nodejs path.normalize & path.join
category: nodejs
description: Nodejs path模块的path.normalize()和path.join()方法
keywords: nodejs,path,path.normalize,path.join
---

以下的内容摘录于 [nodejs官方API文档](https://nodejs.org/docs/latest/api/path.html) 并结合了自己的理解。

如何使用呢？

由于 path 模块是内置的，所以就不需要下载了，直接在代码头部等位置加入 `var path = require(path)` 即可使用！

- path.normalize(p)

    `Normalize a string path` , taking care of '..' and '.' parts.
    
    When multiple slashes are found, they're replaced by a single one; when the path contains a trailing slash, it is preserved. On Windows backslashes are used.
    
        Example:
        
        path.normalize('/foo/bar//baz/asdf/quux/..')
        // returns
        '/foo/bar/baz/asdf'
    
    Note: If the path string passed as argument is a zero-length string then '.' will be returned, which represents the current working directory.

    其实上面的内容，简单的说的话就是要注意如下的几点:
    
    - 如果是 `//` 的话，就会被替换为 `/` 。
    - 如果路径的尾部存在斜线的话就会被保留。
    - 如果传进去的参数是一个空字符串的话，`.` 就会被返回。
    
    看看如下的示例应该就能够明白了:
    
    说明注意事项的前两点：
    
        //test.js
        var path = require('path');
        console.log(path.normalize('/foo//bar/'));
        
        //输出结果
        /foo/bar/
        
    说明注意事项的最后一点:
    
        //test.js
        var path = require('path');
        console.log(path.normalize(''));
        
        //输出结果
        .
        
- path.join([path1][, path2][, ...])

    `Join all arguments together and normalize the resulting path.`
    
    `Arguments must be strings. In v0.8, non-string arguments were silently ignored. In v0.10 and up, an exception is thrown.`
    
        Example:
        
        path.join('/foo', 'bar', 'baz/asdf', 'quux', '..')
        // returns
        '/foo/bar/baz/asdf'
        
        path.join('foo', {}, 'bar')
        // throws exception
        TypeError: Arguments to path.join must be strings
    
    Note: If the arguments to join have zero-length strings, unlike other path module functions, they will be ignored. If the joined path string is a zero-length string then '.' will be returned, which represents the current working directory.
    
    注意事项：
    
    - 从 v0.10 开始，传进去的参数必须是字符串，否则就会抛出异常。
    - 如果参数是空字符串的话，就会被忽略掉。
    - 如果最终合并得到的路径是空字符串的话，`.` 会被返回。

    让我将上面的第一个例子传进去的参数稍微的变动一下，来感受一下这个方法的 `join` 和 `normalize`：
    
        path.join('/foo', 'bar', 'baz/asdf/', 'quux', '..');
        
        输出的结果:
        /foo/bar/baz/asdf
        
欢迎指教=^_^=
