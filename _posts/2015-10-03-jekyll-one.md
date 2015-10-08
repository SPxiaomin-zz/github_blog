---
title: Github & Jekyll 搭建博客(working draft)
category: jekyll 
---

### 知识点简介

### Jekyll 

网上找的博客，有很多都已经过时了，果断花时间看了 [官方文档](http://jekyllrb.com/docs/home/) ，以下的内容摘录于官方文档并结合了自己的理解。

- Front Matter 
 
    [fromt matter 官方文档](http://jekyllrb.com/docs/frontmatter/).

    学习这个之前可以看看我写的 yaml 入门学习笔记 <http://spxiaomin.github.io/github_blog/yaml/2015/10/05/yaml-one.html>，不然的话配置的时候有可能会写错。
    
    使用的原因： Any file that contains a YAML front matter block will be processed by Jekyll as a special file. 也就是说，在生成网站之前，使用了 front matter 的文件将会进行预处理， Liquid tags and variables 将会被替换。如果在文件的头部没有这个东西的话，文件就不会进行解析，原来是什么样子就是什么样子。
    
    使用的注意事项：The front matter must be the first thing in the file and must take the form of valid YAML set between triple-dashed lines. 
    
    在 triple-dashed lines 之间可以使用的内容：you can set predefined variables (see below for a reference) or even create custom ones of your own. 
    
    使用的好处：you can set predefined variables or even create custom ones of your own. These variables will then be available to you to access using Liquid tags both further down in the file and also in any layouts or includes that the page or post in question relies on.
    
    其实 triple-dashed lines 之间的内容是可选的：If you want to use Liquid tags and variables but don’t need anything in your front matter, just leave it empty! The set of triple-dashed lines with nothing in between will still get Jekyll to process your file. (This is useful for things like CSS and RSS feeds!)
    
    下面介绍一下 triple-dashed lines 之间我使用到的一些东西，其它的话，自己去官方文档看吧：
    
    predefined global variables
    
    - layout:
    
        简单的说一下作用吧，这个变量指定的是使用的是 `_layouts` 目录之下的的那个文件来包含 `_posts` 或者其它目录中的文件内容。还有两点要注意的：Use the layout file name `without` the file extension. Layout files `must` be placed in the  `_layouts` directory.
    
        我觉得上面的话，还是有点难以理解，给你们看看我写的 `_layouts/post.html`:
        
            {% raw %}
            <!DOCTYPE html>
            
            <html lang="zh-CN">
                <head>
                    <meta charset="utf-8">
                    <meta http-equiv="X-UA-Compatible" content="IE=edge">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <meta name="description" content="Jimmy的个人博客">
                    <meta name="keywords" content="Jimmy,blogs,html,css,javscript,js,node,express">
            
                    <title>{{ page.title }}</title>
            
                    <link rel="stylesheet" href="{{ "/public/bower_components/bootstrap/dist/css/bootstrap.min.css" | prepend: site.baseurl }}">
                    <link rel="stylesheet" href="{{ "/public/stylesheets/dest/style.min.css" | prepend: site.baseurl }}">
            
                    <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
                    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
                    <!--[if lt IE 9]>
                      <script src="//cdn.bootcss.com/html5shiv/3.7.2/html5shiv.min.js"></script>
                      <script src="//cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
                    <![endif]-->
                </head>
            
                <body>
                    {{ content }}   //这里就是被 Jekyll 处理过的文件
                </body>
            </html>
            {% endraw %}
            
    - category & categories
    
        这个变量顾名思义就知道是定义文件所属的类别。在 Jekyll 中我们并不需要单独的将某一类别的文件放在一个特定的目录之中，通过设置这个变量之后，when the site is generated ,the post will act as though it had been set with these categories normally. 
        
        讲一下使用的方法吧，看看例子就应该明白了：
        
            category: jekyll
        
            categories: [jekyll, github]
            
        只有第二个设置一个文件属于多个类别的时候，格式要注意，可以是 a yaml list 或者是 a comma-separated string. 如果不懂什么是 yaml list 的话，可以看看我写的 yaml 入门学习笔记。
        
        配置完成了之后，就可以通过 `site.categories` 来访问对应类别的文件了。至于怎么使用的话，看看我写的代码吧：

            {% raw %}
            {% for category in site.categories %}
            <h3>{{ category | first }} <small>[{{ category | last | size }}]</small></h3>
            <ul>
                {% for post in category.last %}
                <li>{{ post.date | date:"%a， %b %d， %y"}} -> <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
                {% endfor %}
            </ul>
            {% endfor %}
            {% endraw %}

        上面的代码中还涉及到了 `filters`，简单的讲一下这个东西的作用吧，其实就是一个方法，接收 `|` 左边的内容作为输入，然后看 `|` 后面还有没有 filter，如果没有了的话，就将处理结果返回。如果还有的话，将处理的结果传给下一个 filter 。上面我提到的那篇关于 liquid 的文档中对这个东西进行了详细的解释，但是个人觉得十分的绕口，还是给你们看看原文吧：
        
        Advanced output: Filters
        
        Output markup takes filters. Filters are simple methods. The first parameter is always the output of the left side of the filter. The return value of the filter will be the new left value when the next filter is run. When there are no more filters, the template will receive the resulting string.
        
        下面是使用到的几个 filter 的解释：
        
        first - get the first element of the passed in array
        
        last - get the last element of the passed in array
        
        size - return the size of an array or string

        
    
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

    break-all    允许在单词内换行。

    keep-all    只能在半角空格或连字符处换行。


