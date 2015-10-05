---
layout: post
title: Front Matter defaults 设置不生效
category: jekyll
---

我使用的是 `Ubuntu15.04`，在看 [Jekyll的官方文档](http://jekyllrb.com/docs/configuration/) 的时候，看到了当在 `post` 或 `page` 中设置同样的 `YAML Front Matter` 的时候，就可以使用到 `_config.yml` 文件来避免设置重复的内容-`layout`、`category`...

但是设置之后，奇怪的问题是为什么没有效果，果断的 Google 了一下，[stackoverflow]() 中有人已经解答了这个问题。

简单的说就是当你在本地运行的时候，当已经通过 `jekyll serve` 启动服务器之后，这个配置文件并不会生效，因为它不属于网站的一部分，只有当重启服务器的时候才会 
