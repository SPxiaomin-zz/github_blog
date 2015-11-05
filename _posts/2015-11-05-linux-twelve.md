---
title: Ubuntu 中的 cp 复制命令学习
category: linux
description: Ubuntu 中的 cp 复制命令学习总结
keywords: ubuntu,cp,复制
---

以下的内容摘录于 鸟哥的linux私房菜 并结合了自己的理解。

语法:

    cp [-adfilprsu] 源文件(source) 目标文件(destination)
    cp [options] source1 source2 source3 ... directory
    
    参数简介:
    -a: 相当于 -pdr (常用)
    -p: 连同文件的属性一起复制过去，而非使用默认属性(备份常用)
    -r: 递归持续复制，用于目录的复制行为(常用)
    -d: 若源文件为连接文件的属性(link file)，则复制链接文件属性而非文件本身；在默认的情况下，是复制文件内容
    
    -f: 为强制(force)的意思，若目标文件已经存在且无法开启，则删除后再尝试一次
    -i: 若目标文件(destination)已经存在时，在覆盖时会先询问操作的进行(常用)
    
    -l: 进行硬连接(hard link)的连接文件创建，而非复制文件本身
    -s: 复制成为符号链接文件(symbolic link)，即 “快捷方式” 文件
    
    -u: 若 destination 比 source 旧才更新 destination
    
    最后需要注意的，如果源文件有两个以上，则最后一个目的文件一定要是 "目录" 才行！
    
欢迎指教=^_^=
