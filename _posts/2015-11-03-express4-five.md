---
title: express4.x express-session 模块学习总结
category: express4.x
description: express4.x express-session 模块学习总结
keywords: express,express4.x,express-sesssion,session
---

以下的内容摘录于 <https://github.com/expressjs/session> 并结合了自己的理解。

暂时对这个模块中涉及的内容有些东西还是无法理解，暂时只介绍自己理解了以及使用到了的部分，日后再补充。

- Installation

        sudo npm install --save express-session  // 我使用的是 Ubuntu15.04 ，所以需要加上 sudo 超级用户权限
    
- API

    看个例子：

        var session = require('express-session');
        app.use(session({
            secret: 'secret',
            resave: false,
            saveUninitialized: false
        });
        
        // 后面就可以使用 req.session 访问 session 存储的内容了

    session(options)
    
    create a session middleware with the given options.
    
    `Note: Session data is not saved in the cookie itself, just the session ID. Session data is stored server side.`
    
    Warning: `The default server-side session storage, MemoryStore, is purposely not designed for a production environment.` It will leak memory under most conditions, does not scale past a single process, and is meant for debugging and developing.
    
    - options(只讲解使用到了和理解了的部分):
    
        express-session accepts these properties in the options object.
        
        resave: Forces the session to be saved back to the sessoin store, even if the session was never modified during the request. `The default value is true, but using the default has been deprecated, as the default will change in the future.` Please research into this setting and choose what is appropriate to your use-case.
        
        saveUninitialized: Forces a session that is 'uninitialized' to be saved to the store. `The default value is true, but using the default has been deprecated, as the default will change in the future. `Please research into this setting and choose what is appropriate to your use-case.
        
        secret(`required option`): This is the secret used to sign the session ID cookie. This can be either a string for a single secret, or an array of multiple secrets. If an array of secrets is provided, only the first element will be used to sign the session ID cookie, while all the elements will be considered when verifying the signature in requests.
        
        store: The session store instance, defaults to a new `MemoryStore` instance.
        
    - req.session
    
        To store or access session data, simply use the request propery `req.session`, which is (generally) serizlized as JSON by the store, so nested are typically fine.
        
- example:

    A simple example using express-session to store page views for a user.
    
        // app.js
        var express = require('express');
        var parseurl = require('parseurl'); //解析路由，用到了 memoization 技术缓存
        var logger = require('morgan');  //请求路由记录
        var session = require('express-session');
        
        var routes = require('./routes/index.js');
        
        var app = express();
        
        app.use(logger('dev'));
        app.use(session({
            secret: 'secret',
            resave: false,
            saveUninitialized: false
        }));
        
        app.use(function(req, res, next) {
            var views = req.session.views;
            
            if ( !views ) {     //如果是第一次访问的话，就初始化对象
                views = req.session.views = {};
            }
            
            var pathname = parurl(req).pathname; //类似于 nodejs 内部模块 url，这个模块对 url 进行了包装，采用 memoization 实现缓存
            
            views[pathname] = ( views[pathname] || 0 ) + 1;  
            
            next();  //别忘记了这行代码，继续交给后续的 middleware 处理
        });
        
        app.use('/', routes);
        
        app.listen(3000, function(req, res, next) {
            console.log('App started on Port 3000');
        });
        
        // routes/index.js
        var express = require('express');
        var router = express.Router();
        
        router.route('/foo')
        .get(function(req, res, next) {
            res.send('you viewed this page ' + req.session.views['/foo'] + ' times');
        });
        
        router.route('/bar')
        .get(function(req, res, next) {
            res.send('you viewed this page ' + req.session.views['/bar'] + ' times');
        });
        
        module.exports = router.
        
欢迎指教=^_^=
