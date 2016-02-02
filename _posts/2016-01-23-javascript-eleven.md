---
title: jstips everyday
description: jstips everyday
keywords: jstips everyday
category: javascript
---

- 16/2/1 Map() to the rescue: adding order to Object properties(16/2/2)

    - Map

        Using a new ES6 feature called Map. A Map object iterates its elements in insertion order — a for...of loop returns an array of [key, value] for each iteration.
        
            var myObject = new Map();
            myObject.set('z', 1);
            myObject.set('@', 2);
            myObject.set('b', 3);
            for (var [key, value] of myObject) {
              console.log(key, value);
            ...
            // z 1
            // @ 2
            // b 3
            
    - Hack for old browsers
    
        Mozilla suggest:
        
        So, if you want to simulate an ordered associative array in a cross-browser environment, you are forced to either use two separate arrays (one for the keys and the other for the values), or build an array of single-property objects, etc.
        
            // Using two separate arrays
            var objectKeys = [z, @, b, 1, 5];
            for (item in myObject) {
                myObject[item]
            ...
            
            // Build an array of single-property objects
            var myData = [{z: 1}, {'@': 2}, {b: 3}, {1: 4}, {5: 5}];

- 16/1/31 Avoid modifying or passing arguments into other functions — it kills optimization(16/2/1)

    it is a fairly common practice to convert arguments into an array using the following:
    
        var args = Array.prototype.slice.call(arguments);
    
    A common shorthand for this is :
    
        var args = [].slice.call(arguments);
    
    Unfortunately, passing arguments into any function call will cause the V8 JavaScript engine used in Chrome and Node to skip optimization on the function that does this, which can result in considerably slower performance.
    
    Instead, if you want an array of the arguments that lets you use you need to resort to this:
    
        var args = new Array(arguments.length);
        for(var i = 0; i < args.length; ++i) {
          args[i] = arguments[i];
        }

- 16/1/30 Converting truthy/falsy values to boolean(16/1/31)

    You can convert a truthy or falsy value to true boolean with the !! operator.

- 16/1/29 Speed up recursive functions with memoization(16/1/30)

    define a higher-order function that accepts a function as its argument and returns a memoized version of the function.

        var memoize = function(func){
            var cache = {};
            return function(){
                var key = Array.prototype.slice.call(arguments).toString();
                return key in cache ? cache[key] : (cache[key] = func.apply(this,arguments));
            }
        }
        fibonacci = memoize(fibonacci);

- 16/1/28 Currying vs partial application(16/1/29)

    Curry takes a binary function and returns a unary function that returns a unary function.
    
    curry: (X × Y → R) → (X → (Y → R))
    
    Javascript Code:

        function curry(f) {
          return function(x) {
            return function(y) {
              return f(x, y);
            }
          }
        }

    partApply takes a binary function and a value and produces a unary function.
    
    partApply : ((X × Y → R) × X) → (Y → R)
    
    Javascript Code:

        function partApply(f, x) {
          return function(y) {
            return f(x, y);
          }
        }

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
