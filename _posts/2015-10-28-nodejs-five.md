---
title: nodejs __dirname & process.cwd 得知目录
category: nodejs
description: nodejs 通过 __dirname 和 process.cwd 得知目录
keywords: nodejs,__dirname,process.cwd
---

`__dirname` 和 `process.cwd` 这两个都是全局的，意味着可以在任何地方使用到这两个东西。

__dirname 表示的是 `当前执行脚本` 所在的目录。

process.cwd 返回的是 `当前进程` 的工作目录。



看看例子BA：

    //  /home/gujunmin/test.js
    console.log(__dirname);
    console.log(process.cwd());
    
    输出的结果:
    /home/gujunmin/test
    /home/gujunmin/test
    
是不是懂了呢？

欢迎指教=^_^=
