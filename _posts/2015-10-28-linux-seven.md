---
title: Ubuntu 中的 xargs 参数代换
category: linux
description: Ubuntu 中的 xargs 参数代换
keywords: Ubuntu,xargs
---

以下的内容摘录于 鸟哥的linux私房菜 并结合了自己的理解。

首先介绍以下这个命令的作用吧：

这个玩意儿呢就是用来产生某个命令的参数。更具体的说就是 xargs 可以读入 stdin 的数据作为命令的参数，并且以空格符或断行字符进行分隔，将 stdin 的数据分割成为 arguments。`就是因为以空格符作为分隔，所以，如果有一些文件名或者是其它意义的名词内含有空格符的时候，xargs 就可能会发生误判了。` 要格外的小心啦！

先来简单的看一下语法：

    xargs [-epn] command
    -e: 这个是 EOF(end of file) 的意思。后面 `紧接` 一个字符串，当 xargs 分析到这个字符串的时候，就不在继续的读取 stdin 的内容了。
    -p: 在执行命令的参数的时候，都会询问用户是否要执行。输入 y 并按下 enter 即可执行。
    -n: 限次每次传输给 command 的参数个数。
    
下面看个 `-p` 的使用例子：

    →  ~/Learn/exercises ✗✗✗ find . -name index.js | xargs -p node flip.js 
    node flip.js ./value/index.js ./curry/index.js ./invert-tree/index.js ./merkle/index.js ./memoize/index.js ./flatten/index.js ./debounce/index.js ./async/answers/index.js ./async/index.js ./morse-code/index.js ./throttle/index.js ./map/index.js ./once/index.js ./middleware/index.js ./throttle-promises/index.js ./binary-search/index.js ./flatten-thunk/index.js ./sort/index.js ./jasmine-async/index.js ?...y     //注意： 最后我输入了 y 字符
    
上面的例子就是使用 [node进行加密和解密文件内容的代码](http://spxiaomin.github.io/github_blog/nodejs/2015/10/11/nodejs-one.html) 执行过程，由于一次可以同时加密或解密多个文件，于是便将所有的文件都找出来一次执行了。

上面使用到了 [find](http://spxiaomin.github.io/github_blog/linux/2015/10/28/linux-six.html) 的命令将所有的 index.js 文件找出来，一次性进行加密或解密工作，如果要是一个一个找出来的话，如果文件数目比较少的话倒没什么，如果文件数目比较多并且还分布在不同的目录中，要是不累死你，就怪了 ╮(╯▽╰)╭  ！

其它的参数的话，目前暂时用不到，了解了解即可，暂时就不介绍了！

欢迎指教=^_^=
