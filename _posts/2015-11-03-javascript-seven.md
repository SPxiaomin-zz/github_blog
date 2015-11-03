---
title: Javascript Array toString() toLocaleString() valueOf() 方法
category: javascript
description: Javascript Array toString() toLocaleString() valueOf() 方法学习总结
keywords: javascript,js,Array,toString,toLocaleString,valueOf
---

以下的内容摘录于 红皮书 并结合了自己的理解。

先上例子:

    #!/usr/bin/env node
    
    var colors = ['red', 'blue', 'green'];
    
    console.log(colors.toString());   //red,blue,green
    console.log(colors.toLocaleString());  //red,blue,green
    console.log(colors.valueOf()); //[ 'red', 'blue', 'green' ]
    
从上面的例子应该就可以看出来如下的东西:

toString() 和 toLocaleString(): 返回由数组中的每个值的字符串形式拼接而成的一个以逗号分隔的字符串。唯一的区别是前者会调用数组中每一项的 toString() 方法，后者会调用数组中每一项的　toLocaleString() 方法。

valueOf(): 返回的还是原来的数组。

欢迎指教=^_^=
