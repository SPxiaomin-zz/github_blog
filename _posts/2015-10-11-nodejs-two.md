---
title: process.argv 的详细解释
category: nodejs
---

以下的内容摘录于 nodejs开发指南，并结合了自己的理解。

process.argv 这个代表的是命令行参数数组。

还是看例子比较的容易理解：

源代码文件：

    //test.js
    #!/usr/bin/env node
    console.log(process.argv);
    
输出的结果如下

    →  ~ ✗✗✗ node test.js hello world
    [ '/home/gujunmin/.nvm/versions/node/v4.1.1/bin/node',
      '/home/gujunmin/test.js',
      'hello',
      'world' ]

我的操作系统是 `Ubuntu15.04`，数组的第一项是 node 的安装路径，我使用的是 `nvm` 进行安装的；数组的第二项是被运行的脚本的绝对路径；从第三个元素开始之后的项就是命令的运行参数了。

欢迎指教=^_^=
