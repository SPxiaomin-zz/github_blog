---
title: nodejs 加密和解密代码文件
category: nodejs
---

偶然发现了一个练习 javascript 的 [代码库](https://github.com/kolodny/exercises)，发现那个外国人还真的挺牛逼的，将题目的解答放在了 solutions 分支上面，题目放在 master 分支上面，然而他并没有告诉你解答放在 solutions 分支上面，并且当我发现有 solutions 分支的时候，竟然还发现代码被加密了... 

solutions 分支上面的 readme.md 文件内容：

READ THIS FIRST

Hello there, you seem to have quite an exploratory personality.
Anyway if you found this place, you probably can figure out how to get to the solutions.
Please don't publicize this branch, if people really want to know how to solve something then they'll find this themselves or ask someone else.

If you do contribute a challenge, please also have a similar branch on your fork with a similar setup (some obscurity), although it isn't required.

先看一下加密的代码文件吧：

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

        fs.readFile(filename[, options], callback)

    filename String

    options Object | String
    
    - encoding String | Null default = null
    
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
    
        fs.readFileSync(filename[, options])
    Synchronous version of fs.readFile. Returns the contents of the filename.
        
    If the encoding option is specified then this function returns a string. Otherwise it returns a `buffer`.
        
        fs.writeFile(filename, data[, options], callback)
    
    filename String
    
    data String | Buffer
    
    options Object | String
    
    - encoding String | Null default = 'utf8'
    
    - mode Number default = 0o666
    
    - flag String default = 'w'
    
    callback Function

    Asynchronously writes data to a file, replacing the file if it already exists. data can be a string or a buffer.

    The encoding option is ignored if data is a buffer. It defaults to 'utf8'.

    Example:

        fs.writeFile('message.txt', 'Hello Node.js', function (err) {
          if (err) throw err;
          console.log('It\'s saved!');
        });

    `If options is a string, then it specifies the encoding`. Example:

        fs.writeFile('message.txt', 'Hello Node.js', 'utf8', callback);
    
        fs.writeFileSync(filename, data[, options])

    The synchronous version of fs.writeFile. Returns undefined.

