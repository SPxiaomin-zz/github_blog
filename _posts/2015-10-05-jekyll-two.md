---
layout: post
title: Front Matter defaults 设置以及本地运行生效问题
category: jekyll
---

先介绍下 `default` 的设置问题吧，[官方文档](http://jekyllrb.com/docs/configuration/) 真的写的很详细了。下面的内容摘录于官方文档并结合了自己的理解。

Front Matter defaults

Using YAML Front Matter is one way that you can specify configuration in the pages and posts for your site. Setting things like a default layout, or customizing the title, or specifying a more precise date/time for the post can all be added to your page or post front matter.

Often times, you will find that you are repeating a lot of configuration options. Setting the same layout in each file, adding the same category - or categories - to a post, etc. You can even add custom variables like author names, which might be the same for the majority of posts on your blog.

Instead of repeating this configuration each time you create a new post or page, Jekyll provides a way to set these defaults in the site configuration. To do this, you can specify site-wide defaults using the `defaults` key in the `_config.yml` file in your projects root directory.

The defaults key holds an array of scope/values pairs that define what defaults should be set for a particular file path, and optionally, a file type in that path.

Let’s say that you want to add a default layout to all pages and posts in your site. You would add this to your `_config.yml` file:

    defaults:
      -
        scope:
          path: "" # an empty string here means all files in the project
        values:
          layout: "default"
          
Here, we are scoping the values to any file that exists in the scopes path. Since the path is set as an empty string, it will apply to all files in your project. You probably don’t want to set a layout on every file in your project - like css files, for example - so you can also specify a type value under the scope key.

    defaults:
      -
        scope:
          path: "" # an empty string here means all files in the project
          type: "posts" # previously `post` in Jekyll 2.2.
        values:
          layout: "default"
          
Now, this will only set the layout for files where the type is posts. The different types that are available to you are `pages`, `posts`, `drafts` or `any collection` in your site. While type is optional, you must specify a value for path when creating a scope/values pair.

As mentioned earlier, you can set multiple scope/values pairs for defaults.

    defaults:
      -
        scope:
          path: ""
          type: "posts"
        values:
          layout: "my-site"
      -
        scope:
          path: "projects"
          type: "pages" # previously `page` in Jekyll 2.2.
        values:
          layout: "project" # overrides previous default layout
          author: "Mr. Hyde"
          
With these defaults, all posts would use the my-site layout. Any html files that exist in the projects/ folder will use the project layout, if it exists. Those files will also have the page.author `liquid variable` set to Mr. Hyde as well as have the category for the page set to project.

但是设置之后，奇怪的问题是为什么没有效果，果断的 Google 了一下，[stackoverflow](http://stackoverflow.com/questions/30610668/jekyll-front-matter-defaults-not-working) 中有人已经解答了这个问题。

简单的说就是当你在本地运行的时候，当已经通过 `jekyll serve` 启动服务器之后，如果再修改这个配置文件的话，配置并不会生效，因为它不属于网站的一部分，只有当 `重启服务器` 的时候才会生效 。

[Jekyll 官网](http://jekyllrb.com/docs/variables/) 对此进行了解释：

Jekyll does not parse changes to _config.yml in watch mode, you must restart Jekyll to see changes to variables.

欢迎指教=^_^=
