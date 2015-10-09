---
title: Ubuntu 中的 tee 命令
category: linux
---

以下的内容摘录于 <http://www.runoob.com/linux/linux-comm-tee.html> 并结合了自己的理解。

tee 作用：

用于读取标准的输入，将其内容输出到标准输出设备，同时保存成文件。

使用语法：

    tee [-ai][--help][--version][filename...]
    
参数简介：

    -a或--append 附加到已经存在的文件内容的末尾，而不是覆盖原来文件中的内容。
    
    -i或--ignore-interrupts 忽略中断信号。
    
    --help 在终端显示帮助文档并退出。
    
    --version 在终端显示版本信息并退出。
    
参数后面的是文件名称，可以多个文件。

欢迎指教=^_^=
