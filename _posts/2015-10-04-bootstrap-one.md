---
title: Bootstrap3.3.5 使用模板简介
category: Bootstrap3.3.5
---

以下的模板来自于 <http://v3.bootcss.com/getting-started/> 并结合了自己的理解。

在放暑假的时候学习了一下 bootstrap3.3.5，刚学完，bootstrap4 就出来了，看了一下发布的 [信息](http://blog.getbootstrap.com/2015/08/19/bootstrap-4-alpha/):

Supporting v3

When we shipped Bootstrap 3, we immediately discontinued all support for v2.x, causing a lot of pain for all our users out there. That was a mistake we won’t be making again. For the foreseeable future, we’ll be maintaining Bootstrap 3 with critical bug fixes and documentation improvements. v3 docs will also continue to be hosted after v4’s final release.

暂时还能用，暂时先用着，等 bootstrap4 final release 出来了再换，再加上 bootstrap4 现在已经 Dropped IE8 support and moved to rem and em units 。

先仔细的看看模板吧，在 title 标签的前面加了两个额外的标签：

    <!DOCTYPE html>
    <html lang="zh-CN">
      <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <meta name="description" content="Jimmy的个人博客">
        <meta name="keywords" content="Jimmy,blogs,html,css,javscript,js,node,express">
        <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
        <title>Bootstrap 101 Template</title>
    
        <!-- Bootstrap -->
        <link href="css/bootstrap.min.css" rel="stylesheet">
    
        <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
        <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
        <!--[if lt IE 9]>
          <script src="//cdn.bootcss.com/html5shiv/3.7.2/html5shiv.min.js"></script>
          <script src="//cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
        <![endif]-->
      </head>
      <body>
        <h1>你好，世界！</h1>
    
        <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
        <script src="//cdn.bootcss.com/jquery/1.11.3/jquery.min.js"></script>
        <!-- Include all compiled plugins (below), or include individual files as needed -->
        <script src="js/bootstrap.min.js"></script>
      </body>
    </html>
    
- html5 文档类型

    由于在 bootstrap 中使用了一些 html5 和 css 属性，为了让这些正常的工作，您需要使用 html5 doctype。如果不使用的话，可能面临一些不一致问题，导致代码不能通过 w3c 标准的验证。

- html lang 属性
    
    这个属性指定了页面所使用的语言以及地区。
    
    <http://cnkp.net/archives/16.html> 这篇博客写得还挺详细的。博文中说它的主要作用是对于搜索引擎、浏览器或其它阅读设备，告诉它这个页面是用什么语言来阅读的。对于英文站、外贸站、或者是想对 google 等搜索引擎更友好的话，还是建议加上这个属性。
    
    这个属性可以指定一个页面或是一个段落的语言，比如 `p lang=""` 。
    
- meta charset 属性

    这个属性是用来指定语言的编码方式，中文我知道的有两种编码方式: gbk utf8。
    
- meta IE=edge 属性值

    这个属性值的作用是 Always use the latest standards rendering mode 。
    
    <http://blogs.msdn.com/b/askie/archive/2009/03/23/understanding-compatibility-modes-in-internet-explorer-8.aspx> 
    
    摘录一段来自 <https://msdn.microsoft.com/en-us/library/dd565650(v=vs.85).aspx> 的原文吧，讲得挺清楚的：
    
    Edge mode tells Internet Explorer to display content in the highest mode available. With Internet Explorer 8, this is equivalent to IE8 mode. If a (hypothetical) future release of Internet Explorer supported a higher compatibility mode, pages set to edge mode would appear in the highest mode supported by that version. Those same pages would still appear in IE8 mode when viewed with Internet Explorer 8.
    
    <http://stackoverflow.com/questions/6771258/whats-the-difference-if-meta-http-equiv-x-ua-compatible-content-ie-edge-e> 又看了一篇，貌似情况有变：
    
    Introducing the “living” Edge document mode

    As we announced in August 2013, we are deprecating document modes as of IE11. With our latest platform updates, the need for legacy document modes is primarily limited to Enterprise legacy web apps. With new architectural changes, these legacy document modes will be isolated from changes in the “living” Edge mode, which will help to guarantee a much higher level of compatibility for customers who depend on those modes and help us move even faster on improvements in Edge. The next major version of IE will still honor document modes served by intranet sites, sites on the Compatibility View list, and when used with Enterprise Mode only.

    Public Internet sites will be rendered with the new Edge mode platform (ignoring X-UA-Compatible). It is our goal that Edge is the "living" document mode from here out and no further document modes will be introduced going forward.
    
    但是目前貌似可以不用管，用吧，骚年！
    
