---
title: jstips everyday
description: jstips everyday
keywords: jstips everyday
category: javascript
---

- 16/1/24 Use === instead of ==

    The == (or !=) operator performs an automatic type conversion if needed. The === (or !==) operator will not perform any conversion. It compares the value and the type, which could be considered faster (jsPref) than ==.

- 16/1/23 Converting to number fast way

    Converting strings to numbers is extremely common. The easiest and fastest (jsPref) way to achieve that would be using the + (plus) operator.
    
        var one = '1';
        
        var numberOne = +one; // Number 1

- 16/1/22 Empty an Array

        var list = [1, 2, 3, 4];
        function empty() {
            //empty your array
            list.length = 0;
        }
        empty();
