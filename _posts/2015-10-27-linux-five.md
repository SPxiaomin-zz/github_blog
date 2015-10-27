---
title: Ubuntu diff 进行文件比较
category: linux
description: Ubuntu中使用diff进行文件比较
keywords: Ubuntu,diff,文件比较
---

以下的内容摘录于 鸟哥的linux私房菜 并结合了自己的理解。

直接看例子吧：

    //a.txt
    hello
    world
    
    //b.txt
    hello
    
接下来输入命令并得到相应的结果：

    →  ~/test ✗✗✗ diff a.txt b.txt 
    2d1 
    < world

看到上面的 `<` 号没有，这个符号代表的是命令行中的第一个文件中的内容，所以使用左尖括号是多么的形象啊！

    →  ~/test ✗✗✗ diff b.txt a.txt
    1a2      //
    > world
    
再看看上面的例子之后，是不是明白了呢？

`左边的文件代表的是你想要比较的文件，右边的文件是比较的基准！`

由于上面的原因，所以第一次比较的时候出现的是 `2d1` ，意思是左边的文件删除第二行(内容就是下面显示的)就和基准文件是一样的了。第二次比较的时候出现的是 `1a2` 意思是左边的文件加上一行(内容就是下面显示的)就和基准文件是一样的了。

修改一下文件

    //a.txt
    hello

    //b.txt
    Hello
    
输入如下的命令并得到结果

    →  ~/test ✗✗✗ diff a.txt b.txt 
    1c1
    < hello
    ---
    > Hello
    
这个就是替换的显示，懂了么？

接下来简单的讲一下语法吧：

    diff [-bBi] from-file to-file
    
    from-file: 一个将要做比较的文件名
    to-tile: 一个作为比较基准的文件名
    -b: 忽略一行当中仅有多余空白的区别(例如 "about me" 与 "about      me"视为相同)
    -B: 忽略空白行的区别
    -i: 忽略大小写的区别

欢迎指教=^_^=
