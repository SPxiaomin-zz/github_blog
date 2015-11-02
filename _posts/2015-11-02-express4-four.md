---
title: express4.x req.baseUrl req.url req.originalUrl 学习总结
category: express4.x
description: express4.x req.baseUrl req.url req.originalUrl 学习总结
keywords: express4.x,req.baseUrl,req.url, req.originalUrl
---

以下的内容摘录于 <http://expressjs.com/4x/api.html#req.baseUrl> 并结合了自己的理解。

- req.baseUrl

    The URL path on which a router instance was mounted. For example:
    
        //routes/index.js
        var express = require('express');
        var router = express.Router();
        
        router.get('/foo', function(req, res, next) {
            console.log(req.baseUrl); // /test
            res.send('ok!');
        });
        
        module.exports = router;
        
        //app.js
        var routes = require('./routes/index');
        app.use('/test', routes);
        
- req.originalUrl req.url

    req.originalUrl is much like req.url; `however, it retains the original request URL.` 
    
    req.url: `the 'mount' path is stripped and is not visible to the middleware function.`
    
    For example:
    
        // routes/index.js
        var express =require('express');
        var router = express.Router();
        
        router.get('/hello', function(req, res, next) {
            console.log(req.originalUrl);  // /test/hello
            console.log(req.url);  // /hello
            console.log(req.baseUrl);  // /test
        });
        
        module.exports = router;
        
        //app.js
        var routes = require('./routes/index');
        app.use('/test', routes);
        
欢迎指教=^_^=
