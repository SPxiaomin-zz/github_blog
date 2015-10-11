---
title: Object 类型的创建和使用
category: javascript
---

以下的内容摘录于红皮书并结合了自己的理解。

- 创建 Object 实例

    创建 Object 实例总共有两种方式。
    
    1. 使用 new 操作符后跟 Object 构造函数：
    
            var person = new Object();
            person.name = "Nocholas";
            person.age = 29;
        
    2. 使用对象字面量表示法：
    
            var person  = {
                name: "Nocholas",
                age: 29
            };
    
        使用对象字面量语法时，属性名也可以使用 `字符串` 。
        
- 访问对象属性

    访问对象的属性有两种方法：
    
    1. 一般的情况下使用点表示法。
    
            console.log(preson.name);  //"Nocholas"
    
    2. 使用方括号表示法：
    
        使用方括号表示法时，应该将要访问的属性以字符串的形式放在方括号中，让我们来访问一下上面定义的对象吧：
        
            console.log(person["name"]);   //"Nocholas"
            
    从功能上面来看，这两种访问对象属性的方法没有任何区别。但方括号语法的主要优点是可以通过变量来访问属性，看看例子吧：
    
        var propertyName = "name";
        console.log(preson[propertyName]);   //"Nocholas"

    还有就是当属性名中包含会导致语法错误的字符，或者属性名使用的是关键字或保留字的使用，也可以使用方括号表示法，看看例子吧：
    
        person["first name"] = "Nocholas";
        由于 "first name" 中包含一个空格，所以不能使用点表示法来访问它。然而，属性名中是可以包含非字母非数字的，这时候就可以使用方括号表示法来访问他们。
        
欢迎指教=^_^=
