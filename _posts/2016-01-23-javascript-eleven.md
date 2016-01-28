---
title: jstips everyday
description: jstips everyday
keywords: jstips everyday
category: javascript
---

- 16/1/27 Short circuit evaluation in JS(16/1/28)

        var test = true;
        var isTrue = function(){
          console.log('Test is true.');
        };
        var isFalse = function(){
          console.log('Test is false.');
        };

    Using logical AND - &&.

        // A normal if statement.
        if(test){
          isTrue();    // Test is true
        }
        
        // Above can be done using '&&' as -
        
        ( test && isTrue() );  // Test is true

    Using logical OR - ||.

        test = false;
        if(!test){
          isFalse();    // Test is false.
        }
        
        ( test || isFalse());  // Test is false.

    The logical OR could also be used to set a default value for function argument.

        function theSameOldFoo(name){
            name = name || 'Bar' ;
            console.log("My best friend's name is " + name);
        }

    The logical AND could be used to avoid exceptions when using properties of undefined. Example:-

        var dog = {
          bark: function(){
             console.log('Woof Woof');
           }
        };
        
        // Calling dog.bark();
        dog.bark(); // Woof Woof.
        
        //But if dog is not defined, dog.bark()
        // will raise an error
        // "Cannot read property 'bark' of undefined."
        // To prevent this, we can you &&.
        
        dog && dog.bark();   
        // This will only call dog.bark(),
        // if dog is defined.

- 16/1/24 Use === instead of ==(16/1/27)

    The == (or !=) operator performs an automatic type conversion if needed. The === (or !==) operator will not perform any conversion. It compares the value and the type, which could be considered faster (jsPref) than ==.

- 16/1/23 Converting to number fast way(16/1/26)

    Converting strings to numbers is extremely common. The easiest and fastest (jsPref) way to achieve that would be using the + (plus) operator.
    
        var one = '1';
        
        var numberOne = +one; // Number 1

- 16/1/22 Empty an Array(16/1/25)

        var list = [1, 2, 3, 4];
        function empty() {
            //empty your array
            list.length = 0;
        }
        empty();
