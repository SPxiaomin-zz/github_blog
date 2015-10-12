---
title: 加密和解密代码
category: nodejs
---

偶然发现了一个练习 javascript 的 [代码库](https://github.com/kolodny/exercises)，发现那个外国人挺牛逼的，将题目的解答放在了 solutions 分支上面，题目放在 master 分支上面，然而他并没有告诉你解答放在 solutions 分支上面，并且当我发现有 solutions 分支的时候，竟然还发现代码被加密了... 

solutions 分支上面的 readme.md 文件内容：

    READ THIS FIRST
    
    Hello there, you seem to have quite an exploratory personality.
    Anyway if you found this place, you probably can figure out how to get to the solutions.
    Please don't publicize this branch, if people really want to know how to solve something then they'll find this themselves or ask someone else.

    If you do contribute a challenge, please also have a similar branch on your fork with a similar setup (some obscurity), although it isn't required.

先看一下加密和解密的代码文件吧：

    #!/usr/bin/env node
    
    // put the next line on top of your answer files
    //}47}$.(}:</}*88})54*q}$.(}/889}).}+(/})54*}7418})5+.(65}714-o3*
    
    var fs = require('fs');
    
    var map = {};
    var str = ' !"#$%&\'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\\]^_`abcdefghijklmnopqrstuvwxyz{|}';
    str.split('').forEach(function(ch, i) {
      map[str[i]] = str[str.length - 1 - i];
    });
    
    process.argv.slice(2).forEach(function(file) {
      var input = fs.readFileSync(file).toString();
    
      var output = input.split('\n').map(function(line) {
        return line.split('').map(function(ch) {
          return map[ch] || ch;
        }).join('');
      }).join('\n');
    
      fs.writeFileSync(file, output);
    
    });
    
知识点讲解：

- nodejs fs API

    [官方文档](https://nodejs.org/api/fs.html#fs_fs_readfilesync_filename_options) 写的十分的详细，果断摘录了下来。

    异步读取文件内容：
 
        fs.readFile(filename[, options], callback)

    filename String

    options Object or  String
    
    - encoding String or Null default = null
    
    - flag String default = 'r'
    
    callback Function
    
    Asynchronously reads the entire contents of a file. Example:
        
        fs.readFile('/etc/passwd', function (err, data) {
          if (err) throw err;
          console.log(data);
        });
        
    The callback is passed two arguments (err, data), where data is the contents of the file.
        
    If no encoding is specified, then the `raw buffer` is returned.
        
    `If options is a string, then it specifies the encoding.` Example:
        
        fs.readFile('/etc/passwd', 'utf8', callback);

    同步读取文件内容：
    
        fs.readFileSync(filename[, options])

    Synchronous version of fs.readFile. Returns the contents of the filename.
        
    If the encoding option is specified then this function returns a string. Otherwise it returns a `buffer`.
    
    异步将内容写入文件：    
   
        fs.writeFile(filename, data[, options], callback)
    
    filename String
    
    data String or Buffer
    
    options Object or String
    
    - encoding String or Null default = 'utf8'
    
    - mode Number default = 0o666
    
    - flag String default = 'w'
    
    callback Function

    Asynchronously writes data to a file, replacing the file if it already exists. data can be a string or a buffer.

    `The encoding option is ignored if data is a buffer. It defaults to 'utf8'.`

    Example:

        fs.writeFile('message.txt', 'Hello Node.js', function (err) {
          if (err) throw err;
          console.log('It\'s saved!');
        });

    `If options is a string, then it specifies the encoding`. Example:

        fs.writeFile('message.txt', 'Hello Node.js', 'utf8', callback);
    
    同步将内容写入文件：
    
        fs.writeFileSync(filename, data[, options])

    The synchronous version of fs.writeFile. Returns undefined.

- process.argv 

    <http://spxiaomin.github.io/github_blog/nodejs/2015/10/11/nodejs-two.html> 我的博客文章上对此做了详细的解释。

- javascript

    Object 类型的创建和使用方法： <http://spxiaomin.github.io/github_blog/javascript/2015/10/11/javascript-five.html>

    String 类型的 split() 方法： <http://spxiaomin.github.io/github_blog/javascript/2015/10/11/javascript-one.html>
    
    Array 类型的 迭代方法： <http://spxiaomin.github.io/github_blog/javascript/2015/10/11/javascript-two.html>
    
    Array 类型的 slice() 方法： <http://spxiaomin.github.io/github_blog/javascript/2015/10/11/javascript-three.html>
    
    Array 类型的 join() 方法： <http://spxiaomin.github.io/github_blog/javascript/2015/10/11/javascript-four.html>
    
经过上面知识点的简要介绍，是不是懂得了这个程序能够同时进行加密和解密的缘由了呢？

不懂了也关系，接下来我就一行一行代码来进行解释：

    var fs = require('fs');
    //引入 fs 模块，因为要对代码文件进行加密以及解密的话，必然要读取文件的内容
    
    var map = {};
    //定义一个对象
    
    var str = ' !"#$%&\'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\\]^_`abcdefghijklmnopqrstuvwxyz{|}';
    //总共有94个字符
    
    str.split('').forEach(function(character, index) {
        map[str[index]] = str[str.length - 1 - index];
    });
    //首先通过 split 方法将上面的94个字符全部分开来，然后一个一个的按顺序保存到数组中去。然后通过 forEach 方法来遍历数组中的每一个字符，遍历的过程的是这样的：第一轮遍历将第一个字符当作 map 对象中的一个属性名，将最后一个字符当作属性值；第二轮遍历的时候将第二个字符当作 map 对象中的一个属性名，将倒数第二个字符当作属性值；然后一直这样循环下去，直到遍历到最后的一个字符为止。
    
    process.argv.slice(2).forEach(function(file) {
        //process.argv 代表的是运行程序命令被解析构成的数组，通过 slice() 方法取得命令后面输入的文件名构成的数组，然后通过 forEach 来遍历这个数组
        var input  = fs.readFileSync(file).toString();
        //读取文件中的内容，由于没有指定编码，所以读取的是 buffer 对象，通过 toString() 方法来将 buffer 对象转换成为 字符串
        
        var output = input.split('\n').map(function (line) {
            return line.split('').map(function (character) {
                return map[character] || character;
            }).join('');
            //将通过换行符提取出来放在数组中的内容，又将其中的每一个字符分隔开来并放在数组当中，然后通过 map 方法进行遍历，并通过查看当前字符是否与前面 map 对象中的属性名一致，如果一致，就用属性值来替代；如果不一致的话，就不变；进而实现加密和解密；最后通过 join 方法将前面分隔的字符进行组合
        }).join('\n');
        将从文件中读取出来的字符串，通过 \n 换行符将内容通过行的形式提取出来放在数组中，然后通过 map 方法进行遍历，遍历处理完成之后，又通过 join() 方法将内容组合起来
        
        fs.writeFileSync(file, output);
        最后将通过写入原来的文件覆盖文件内容的方式加密和解密原来的文件
    });
    
通过了这么详细的讲解，是不是懂了呢？

最后简单的讲解一下使用的方法吧：

    node [上面的代码所属的文件名称] [你想加密以及解密的文件名称...]

欢迎指教=^_^=
