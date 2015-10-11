---
title: Array & String 的 slice 方法
category: javascript
---

以下的内容摘录于 红皮书，并结合了自己的理解。

之所以在这里同时涉及到两个类型的方法是因为：

1. 这个方法不但在两个类型当中同名，
2. 而且作用也十分的相似。

开始分别介绍这些方法啰：

- Array slice() 

    作用：
    
    这个方法能够基于当前数组中的一或多个项创建一个新的数组。
    
    参数简介：
    
    这个方法可以接受一或两个参数，即要返回项的起始和结束位置。
    
    在只有一个参数的情况下，slice() 方法返回从该参数指定位置开始到当前数组末尾的所有项。
    
    如果有两个参数，该方法返回起始和结束位置之间的项--但是要注意的是：结束位置的项并不包含在其中。
    
    还有一点要注意的是 slice 方法不影响原始数组。
    
    看看例子吧：
    
        var colors = ["red", "green", "blue", "yellow", "purple"];
        var colors2 = colors.slice(1);
        var colors3 = colors.slice(1, 4);
        
        console.log(colors2);  //["green", "blue", "yellow", "purple"]
        console.log(colors3);  //["green", "blue", "yellow"]
        
    当传入的参数是负数的情况下可以通过 `用数组的长度加上该数` 来转化为正数。接下来就和上面的处理方式是一样的了。但是如果结束位置小于起始位置的话，则返回空数组。
    
- String slice()

    作用：
    
    这个方法基于子字符串创建新的字符串。
    
    参数简介：
    
    可以接受一个或两个参数。
    
    第一个参数指定子字符串的开始位置。
    
    第二个参数指定的是子字符串最后一个字符 `后面` 的位置。
    
    这个方法不会修改字符串本身的值，对原始的字符串没有任何的影响。
    
    看看例子吧：
    
        var stringValue = "hello world";
        
        console.log(stringValue.slice(3));        //"lo world"
        
        console.log(stringValue.slice(3, 7));     //"lo w"
        
    如果传入的参数是负值的话，可以通过用 `数组的长度加上该数` 来转换为正数。接下来的处理方式就和上面的是一样的了。
    
看完了上面对两种方式的介绍是不是和我一样觉得，真的长得好像！

欢迎指教=^_^=
    
