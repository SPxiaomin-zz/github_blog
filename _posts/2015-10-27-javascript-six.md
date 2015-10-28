---
title: javascript Math.random() 方法
category: javascript
description: javascript Math.random() 方法
keywords: javascript,js,Math.random
---

以下的内容摘录于红皮书并结合了自己的理解。

作用：

Math.random() 这个方法返回 `[0,1)` 这个范围之间的一个随机数。

使用示例：

    function selectFrom(lowerValue, upperValue) {
        var choices = upperValue - lowerValue + 1;
        return Math.floor(Math.random() * choices + lowerValue);
    }
    
    var num = selectFrom(2, 10);
    console.log(num); //输出的是介于2和10之间的 (包括2和10) 的一个数值
    
上面的这个函数可以从你给出的最大值和最小值之间任意的选取一个值！

欢迎指教=^_^=
