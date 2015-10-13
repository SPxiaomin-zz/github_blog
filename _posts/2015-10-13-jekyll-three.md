---
title: Listen error 的解决方法
category: jekyll
---

随着文件数量的增加，在终端中输入 jekyll serve 启动服务器的时候，突然发现了一个错误：

    FATAL: Listen error: unable to monitor directories for changes.
    Visit https://github.com/guard/listen/wiki/Increasing-the-amount-of-inotify-watchers for info on how to fix this.
    
这个错误提示信息讲得还挺详细的，告诉了我们解决方法的网址，果断打开，看了之后，我心里默默的说了一句，原来如此！

我使用的是 `Ubuntu15.04`， 解决方案是在终端输入如下的命令：

    echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
    
然后问题就解决了，重新输入 jekyll serve 之后就可以重启服务器了。

原因：

Listen uses inotify by default on Linux to monitor directories for changes.There is a system limit on the number of files you can monitor.When this limit is not enough to monitor all files inside a directory, the limit must be increased for Listen to work properly.

欢迎指教=^_^=
