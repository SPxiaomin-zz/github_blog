---
title: Github & Jekyll 搭建博客(working draft)
category: jekyll 
---

### 知识点简介

### Jekyll 

网上找的博客，有很多都已经过时了，果断花时间看了 [官方文档](http://jekyllrb.com/docs/frontmatter/) ，以下的内容摘录于官方文档并结合了自己的理解。

- Front Matter 

    学习这个之前可以看看我写的 yaml 入门学习笔记 <http://spxiaomin.github.io/github_blog/yaml/2015/10/05/yaml-one.html>，不然的话配置的时候有可能会写错。
    
    使用的原因： Any file that contains a YAML front matter block will be processed by Jekyll as a special file. 也就是说，在生成网站之前，使用了 front matter 的文件将会进行预处理， Liquid tags and variables 将会被替换。
    
    使用的注意事项：The front matter must be the first thing in the file and must take the form of valid YAML set between triple-dashed lines. 
    
    在 triple-dashed lines 之间可以使用的内容：you can set predefined variables (see below for a reference) or even create custom ones of your own. 
    
    使用的好处：
    
### Bootstrap3.3.5



### CSS3

以下内容摘录于 [w3school](http://www.w3school.com.cn/css3/css3_text_effect.asp) 。

- css3 word-wrap 
    
    作用：

    允许长单词换行到下一行。

    语法：
    
        word-wrap: normal|break-word;
    
    值    描述

    normal    只在允许的断字点换行（浏览器保持默认处理）。

    break-word    在长单词或 URL 地址内部进行换行。
    
- css3 word-break

    作用：
    
    word-break 属性规定自动换行的处理方法。
    
    语法：
    
        word-break: normal|break-all|keep-all;

    值    描述

    normal    使用浏览器默认的换行规则。

    break-all	允许在单词内换行。

    keep-all	只能在半角空格或连字符处换行。


