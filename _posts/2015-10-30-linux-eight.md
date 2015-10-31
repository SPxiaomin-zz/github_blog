---
title: Ubuntu wc 计算文件内容行数、字数、字符数
category: linux
description: Ubuntu 中的 wc 用来计算文件内容行数、字数、字符数
keywords: linux,ubuntu,wc
---

以下的内容摘录于 鸟哥的linux私房菜 并结合了自己的理解。

简单的介绍一下语法:

    wc [-lwn]
    参数简介：
    -l: 仅列出行数
    -w: 仅列出多少个字(英文单字)
    -m: 仅列出多少个字符
    
看看如何使用吧：

    //t.js
    #!/usr/bin/env node
    
    console.log(process.argv);
    
第一种使用方法：

    →  ~/test ✗✗✗ wc t.js
     3  3 48 t.js

第一个是行数，第二个是字数，第三个是字符数。

对于行数的话，还是比较符合我的思维方式，至于单词数和字符数的话，我就不管了，一般情况下用到的机会也不多。

第二种使用方法：

    →  ~/test ✗✗✗ cat t.js | wc 
          3       3      48

至于参数的使用的话，如果需要就直接接在 wc 后面就可以了。

欢迎指教=^_^=
