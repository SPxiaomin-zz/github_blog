---
title: script 执行执行方式的区别(source, sh script, ./script)
category: bash
description: script 使用直接执行的方式和使用source来执行的方式的区别
keywords: script,执行方式,source
---

以下的内容摘录于 鸟哥的linux私房菜 并结合了自己的理解。

`不同的 script 执行方式会造成不一样的结果，尤其对 bash 的执行环境影响很大。`

- 利用直接执行的方式来执行 script

    直接执行指的是:
    
    1. 使用 绝对路径/相对路径/$PATH路径 执行
    2. 使用 bash/sh 执行
    
    使用这些方式执行脚本的时候，其实 script 是在子进程的 bash 内执行的。`当子进程完成后，子进程内的各项变量或操作就会结束而不会传回父进程中。`

- 利用 source 来执行脚本

    这种方式和使用 `.` 执行是一样的，都是在父进程中执行。
    
    `如果在父进程中执行，各项操作都会在原本的 bash 内生效！` 这也是为什么你不注销系统而要让某些写入 ~/.bashrc 的设置生效时，需要使用　`source ~/.bashrc` ，而不能使用 `bash ~/.bashrc` 。
    
欢迎指教=^_^=
