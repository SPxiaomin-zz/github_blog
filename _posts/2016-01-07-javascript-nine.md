---
title: JavaScript DOM 编程艺术（2th) 表单学习总结
description: JavaScript DOM 编程艺术（2th) 表单学习总结
keywords: JavaScript DOM 编程艺术（2th) 表单学习总结
category: javascript
---

- 检测是否支持 `某种类型` 的输入控件

        function inputSupportsType(type) {
            if ( !document.createElement ) {
                return false;
            }
            var input = document.createElement('input');
            input.setAttribute('type', type);   //good
            if ( input.type === 'text' && type !== 'text' ) { //good
                return false;
            }
            return true;
        }

- 检测 `特定的属性`

        function elementSupportsAttribute(elementName, attribute) {
            if ( !document.createElement ) {
                return false;
            }
            var element = document.createElement(elementName);
            return (attribute in element);  //good
        }

- 标签结合与样式设置

    - `label` 与 `input` 使用 `div` 合并在一起
    - `label` `input` 设置成 `block` 使得 `上下` 排列，设置成 `inline-block` 使得 `水平` 排列
    - `fieldset` 设置 `border: 0;` 去除边框
    
- 字段标签

    - 设置鼠标点击事件，使得对应 `id` 的控件实现 `focus`
    - 设置原因：有些浏览器没有实现
    - 代码：
    
            function focusLabels() {
                if ( !document.getElementsByTagName ) {
                    return false;
                }
                var id;
                var labels = document.getElementsByTagName('label');
                for ( var i=0; i<labels.length; i++ ) {
                    id = labels[i].getAttribute('for');
                    if ( id ) {
                        (function(id) {
                            labels[i].onclick = function() {
                                var element = document.getElementById(id);
                                if ( !element ) {
                                    return false;
                                }
                                element.focus(); //good
                            };
                        })(id); //good，借助函数按值传递的特性
                    }
                }
            }

- form 对象学习

    - 定义: 代表的是一个表单
    - 获取: `document.forms`
    - 特性: 
        
        - `document.forms[i].elements` 是一个 `数组`，具有 `length` 属性
        - `document.forms[i].elements` 只关注属于表单元素的元素，如 `input` 、`textarea`
        - `document.forms[i].elements[i].value` 可以通过此方式取得与　`document.forms[i].elements[i].getAttribute('value')`　一样的效果

- 占位字符

    - 设置占位文本
    - 设置原因：有些浏览器不支持 `placeholder` 属性，并且有些浏览器不能正确的识别空的表单字段，从而导致用户不能通过 `Tab` 按键进入空的字段
    - 样式设置: 借助 `class` 属性，设置 `color: grey`
    - 代码：
    
            function resetField(whichform) {
                var element;
                var placeholder;
            
                if ( !Modernizr.input.placeholder ) {
                    for ( var i=0, length=whichform.elements.length; i<length; i++ ) { //good, 在 `pre-loop` 部分取得表单元素的个数，提高性能，避免重复计算
                        element = whichform.elements[i];
                        if ( element.type !== 'submit' ) {
                            placeholder = element.placeholder || element.getAttribute('placeholder'); //good, 不同浏览器对未知属性的实现方式不同
                            if ( placeholer ) {
                                (function(placeholder) {
                                    element.onfocus = function() {
                                        if ( this.value === placeholder ) { //good, 通过 this 取得当前对象
                                            this.className = ''; //good，取得类名的方式
                                            this.value = ''; 
                                        }
                                    };
                                    element.onblur = function() {
                                        if ( this.value === '' ) {
                                            this.className = 'placeholder'; 
                                            this.value = placeholder;
                                        }
                                    };
                                    element.onblur();  //good
                                })(placeholder); //good，借助函数按值传递的特性
                            }
                        }
                    }
                }
            }
            
            function prepareForms() {
                for ( var i=0, length=document.forms.length; i<length; i++ ) {
                    resetField(document.forms[i]);
                }
            }

- 表单验证

    - 设置了 `required` 的表单控件，有时候浏览器不一定支持，需要额外设置脚本进行支持；与此同时可以进行一定的验证，设置了类型的表单控件有的浏览器不一定支持验证功能，这时也需要设置额外的脚本进行支持
    - 代码:
    
            function isFilled(field) {
                if ( field.value.replace(' ', '').length === 0 ) {  //good
                    return false;
                }
                var placeholder = field.placeholder || field.getAttribute('placeholder'); //good
                return (field.value !== placeholder);
            }
            
            
            function isEmail(field) {
                return (field.value.indexOf('@') !== -1 && field.value.indexOf('.') !== -1); //good
            }
            
            
            function validateForm(whichform) {
                var element;
                for ( var i=0, length=whichform.elements.length; i<length; i++ ) { //good
                    element = whichform.elements[i];
                    if ( element.required ) {
                        if ( !isFilled(element) ) {
                            alert('Please fill in the ' + element.name + ' field.');
                            return false;
                        }
                    }
                    if ( element.type === 'email' ) {
                        if ( !isEmail(element) ) {
                            alert('The ' + element.name + ' field must be filled with a valid email address.');
                            return false;
                        }
                    }
                }
                return true;
            }
            
            
            function prepareForms() {
                var thisform;
            
                for ( var i=0, length=document.forms.length; i<length; i++ ) {
                    thisform = document.forms[i];
                    resetField(thisform);
                    thisform.onsubmit = function() {
                        return validateForm(thisform); //good, 通过返回的逻辑值来进一步确定是否进行表单的提交
                    };
                }
            }
            
- 提交表单

        function getXMLObject() {
            if ( typeof XMLHttpRequest === 'undefined' ) { //good，也可以通过 window.XMLHttpRequest 进行检测
                try {
                    return new ActiveXObject('Microsoft.XMLHTTP');
                } catch(error) {
                }
            }
            return new XMLHttpRequest();
        }
        
        function displayAjaxLoading(element) {
            while ( element.hasChildNodes() ) {　//good，检测是否还有孩子节点存在
                element.removeChild(element.lastChild);
            }
        
            var img = document.createElement('img');
            img.setAttribute('src', 'images/loading.gif');
            img.setAttribute('alt', 'loading...');
            element.appendChild(img);
        }
        
        
        function submitFormWithAjax(whichform, thetarget) {
            var xhr = getXMLObject();
            if ( !xhr ) {
                return false;
            }
            displayAjaxLoading(thetarget);
            var dataParts = [];
            var element;
            for ( var i=0, len=whichform.elements.length; i<len; i++ ) { //good
                element = whichform.elements[i];
                dataParts[i] = element.name + '=' + encodeURIComponent(element.value);　//good, 进行编码
            }
            var data = dataParts.join('&');
            xhr.onreadystatechange = function() {  //good, 在 open 之前
                if ( xhr.readyState === 4 ) {
                    if ( xhr.status === 200 ) {
                        var matches = xhr.responseText.match(/<article>([\s\S]+)<\/article>/); //good，正则表达式写的好
                        if ( matches.length > 0 ) {
                            thetarget.innerHTML = matches[1];
                        } else {
                            thetarget.innerHTML = '<p>Oops, there was an error. Sorry.</p>';
                        }
                    } else {
                        thetarget.innerHTML = '<p>' + xhr.status + '</p>';
                    }
                }
            };
            xhr.open('POST', whichform.getAttribute('action'), true); //good, 取属性用的好
            xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');  //good，在 open 和 send 之间
            xhr.send(data);
            return true;
        }
        
        
        function prepareForms() {
            var thisform;
            var article = document.getElementsByTagName('article')[0];
            for ( var i=0, len=document.forms.length; i<len; i++ ) { //good
                thisform = document.forms[i];
                resetField(thisform);
                thisform.onsubmit = function() {
                    if ( !validateForm(this) ) {
                        return false;
                    }
                    if ( submitFormWithAjax(this, article) ) {
                        return false;
                    }
                    return true;
                };
            }
        }

欢迎指教=^_^=
