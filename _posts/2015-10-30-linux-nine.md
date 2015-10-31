---
title: Ubuntu grep egrep 选取包含关键字的行
category: linux
description: Ubuntu 中使用 grep egrep 对一段数据进行分析，选取出具有关键字的那一行
keywords: ubuntu,linux,grep,egrep,选取命令
---

以下的内容摘录于 鸟哥的linux私房菜 并结合了自己的理解。

grep 命令作用：

对数据内容一行一行的进行分析，如果当中有我们所需要的信息的话，就将该行拿出来。

看看语法吧：

    grep [-inv] [-A] [-B] [--color=auto] '需要查找的字符串' filename
    参数简介:
    -i: 忽略大小写的不同，所以大小写视为相同的
    -n: 顺便输出行号
    -v: 反向选择，即显示出没有 '查找字符串' 内容的那一行
    --color=auto: 可以将找到的关键子部分加上颜色显示。我使用的是 Ubuntu15.04，系统默认已经通过 alias grep='grep --color=auto' 将命令进行了别名设置。
    -A: 后面可加数字，为 after 的意思，意思是除了列出该行外，后续的 n 行也列出来
    -B: 后面可加数字，为 before 的意思，意思是除了列出该行外，后续的 n 行也列出来
    对于引号中的内容，为需要查找的字符串，可以使用正则表达式。不过有一点需要注意的是: 由于 `{}` 这两个符号在 shell 中是有特殊意义的，因此，我们必须要使用转义字符 `\` 来让它失去特殊意义才行。但是需要注意的是 grep 仅支持基础正则表达式，如要想要使用扩展型正则表达式，你可以使用 egrep ，语法和 grep 是一样的。
    
    基础正则表达式: ^ $ . \ * [] [n1-n2] [^] \{n,m\}
    扩展型正则表达式: + ? | () ()+
    
看看例子吧：

测试文件内容：

    //t.js
    #!/usr/bin/env node
    
    console.log(process.argv);
    
命令执行和结果显示：

    →  ~/test ✗✗✗ grep 'console' t.js
    console.log(process.argv);
    →  ~/test ✗✗✗ grep -i 'CONSOLE' t.js
    console.log(process.argv);
    →  ~/test ✗✗✗ grep -v 'console' t.js
    #!/usr/bin/env node
    
至于 `-A` 和 `-B` 的话，从字面上并结合上面的例子应该就非常的好理解，我就不举例说明了。我的做法是在 `~/.bashrc` 文件中加上这么一句话: `alias grep='grep --color=auto -A3 -B3 -n'` ，是不是会感觉到特别的方便。

欢迎指教=^_^=
