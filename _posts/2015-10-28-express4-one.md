---
title: express4.x 设置模板引擎使得 ejs 可以解析 html 后缀的文件
category: express4.x
description: express4.x 设置模板引擎是的 ejs 可以解析 html 后缀的文件
keywords: express,express4.x,ejs解析html文件
---

以下的内容摘录于 [express.js官方API文档](http://expressjs.com/4x/api.html#app.engine) ，并结合了自己的理解。

Application Settings
    
The following application settings affects the behavior of the application.
    
    Property: views
    
    Type: String or Array
    
    Value: A directory or an array of directories for the application's views. If an array, the views are looked up in the order they occur in the array.
    
    Default: process.cwd() + '/views'
    
从上面的一大段英文可得知，通过设置 `views` 的值即可相应的设置 views 文件放置的位置。具体应该怎么做呢？看看下面吧：

    app.set('views', path.join(__dirname, 'views'));
    
接下来让我们来设置解析 
    
    
