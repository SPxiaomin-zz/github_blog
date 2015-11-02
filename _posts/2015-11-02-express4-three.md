---
title: express4.x Router 学习总结
category: express4.x
description: express4.x Router 路由控制学习总结
keywords: express4.x,route,router,路由控制
---

以下的内容摘录于 <http://expressjs.com/4x/api.html#router> 并结合了自己的理解。

A router behaves like middleware itself, so you can use it as an argument to app.use().

`The top-level express object has a Router() function that creates a new router object.`

create a new router as follows:

    var router = require('express').Router([options]);
    
options:

property: caseSensitive; Description: Enable case sensitive; Default: Disabled by default, treating `/Foo` and `/foo` as the same.

property: strict; Description: Enable strict routing; Default: Disabled by default, `/foo` and `/foo/` are treated the same by the router.

- router.METHOD(path, [callback,...]callback)

    The router.METHOD methods provide the routing functionality in Express, where METHOD is one of the HTTP methods, such as GET, PUT, POST, and so on, in lowercase. Thus, the actual methods are router.get(), router.post(), router.put(), and so on.
    
    You can provide multiple callbacks, and all are treated equally, and behave just like middleware, except that these callbacks may invoke next('route') to bypass the remaining route callback(s). You can use this mechanism to perform pre-conditions on a route then pass control to subsequent routes when there is no reason to proceed with the route matched.
    
    `Express translates the path strings to regular expressions, used internally to match incoming requests. Query string are not considered when performing these matches, for example 'GET /' route match '/', as would 'GET /?name=tobi'.`
    
    The path strings can also use regular expressions.
    
- router.route(path)

    Returns an instance of a single route which you can then use to handle HTTP verbs with optional middleware. `Use router.route() to avoid duplicate route naming and thus typo errors.`
    
        var express = require('express');
        var router = express.Router();
        
        router.route('/test')
        .get(function(req, res, next) {
            res.send('hello');
        })
        .post(function(req, res, next) {
            res.end('world');
        });
        
    This approach re-uses the single '/test' path and add handlers for various HTTP methods.

欢迎指教=^_^=
