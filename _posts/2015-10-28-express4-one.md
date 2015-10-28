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
    
接下来让我们来设置 ejs 引擎用来解析文件名后缀为 .html 的文件：

    app.engine(ext, callback)
    Registers the given template engine callback as ext.
    
    By default, Express will require() the engine based on the file extension. For example, if you try to render a “foo.jade” file, Express invokes the following internally, and caches the require() on subsequent calls to increase performance.
    
    app.engine('jade', require('jade').__express);
    Use this method for engines that do not provide .__express out of the box, or if you wish to “map” a different extension to the template engine.
    
    For example, to map the EJS template engine to “.html” files:
    
    app.engine('html', require('ejs').renderFile);
    In this case, EJS provides a .renderFile() method with the same signature that Express expects: (path, options, callback), though note that it aliases this method as ejs.__express internally so if you’re using “.ejs” extensions you don’t need to do anything.
    
    Some template engines do not follow this convention. The consolidate.js library maps Node template engines to follow this convention, so they work seemlessly with Express.
    
    var engines = require('consolidate');
    app.engine('haml', engines.haml);
    app.engine('html', engines.hogan);

通过上面那么一大段话的解释，应该就可以明白到，通过使用 `app.engine('html', require('ejs').renderFile);` 之后，我们就可以使用 ejs 模板引擎来解析我们的 html 文件了。

还有一个小小的技巧，看看下面的代码应该就可以明白怎么做了:

    app.set('view engine', 'html');

通过上面的这一行代码的设置之后，就可以这样使用 `res.render('index');` 而不需要 `res.render('index.html');` 这样来使用了！

是不是懂了呢？

欢迎指教=^_^=
