---
title: jstips everyday
description: jstips everyday
keywords: jstips everyday
category: javascript
---

- 16/2/14 Calculate the Max/Min value from an array(16/2/15)

    There are two methods to find Max and Min numbers from an argument list of numbers but they does not support Arrays natively.
    
        Math.max(1, 2, 3, 4); // 4
        Math.min(1, 2, 3, 4); // 1
    
    apply() allows you to use built-ins functions to find Max Min value in an Array.
    
        var numbers = [1, 2, 3, 4];
        Math.max.apply(null, numbers) // 4
        Math.min.apply(null, numbers) // 1
    
    Another way more easier is with the new spread operator.
    
        var numbers = [1, 2, 3, 4];
        Math.max(...numbers) // 4
        Math.min(...numbers) // 1

- 16/2/13 Know the passing mechanism(16/2/14)

    Example 1
    
        var me = {                  // 1
            'partOf' : 'A Team'
        }; 
        
        function myTeam(me) {       // 2
        
            me = {                  // 3
                'belongsTo' : 'A Group'
            }; 
        }   
        
        myTeam(me);     
        console.log(me);            // 4  : {'partOf' : 'A Team'}
    
    Example 2
    
        var me = {                  // 1
            'partOf' : 'A Team'
        }; 
        
        function myGroup(me) {      // 2
            me.partOf = 'A Group';  // 3
        } 
        
        myGroup(me);
        console.log(me);            // 4  : {'partOf' : 'A Group'}

- 16/2/12 Use destructuring in function parameters(16/2/13)

        var sayHello = function({ name, surname }) {
          console.log(`Hello ${name} ${surname}! How are you?`);
        };
        
        sayHello({
          name: 'John',
          surname: 'Smith'
        });

- 16/2/11 Preventing Unapply Attacks(16/2/12)

    By overriding the builtin prototypes, attackers can rewrite code to expose and change bound arguments. 
    
    By using `Object.freeze` , making an object immutable, you prevent any overriding of the builtin object prototypes.
    
        (function freezePrototypes() {
          if (typeof Object.freeze !== 'function') {
            throw new Error('Missing Object.freeze');
          }
          Object.freeze(Object.prototype);
          Object.freeze(Array.prototype);
          Object.freeze(Function.prototype);
        }());

- 16/2/10 Array Average And Median(16/2/11)

    get the average

        let values = [2, 56, 3, 41, 0, 4, 100, 23];
        let sum = values.reduce((previous, current) => current += previous);
        let avg = sum / values.length;
        // avg = 28

    get the median
 
        let values = [2, 56, 3, 41, 0, 4, 100, 23];
        values.sort((a, b) => a - b);
        let middle = Math.floor(values.length / 2);
        let median = values[middle];
        // median = 23
        
        let values = [2, 56, 3, 41, 0, 4, 100, 23];
        values.sort((a, b) => a - b);
        let median = values[values.length >> 1];
        // median = 23

- 16/2/9 Using JSON.Stringify(16/2/10)

        var obj = {
            'prop1': 'value1',
            'prop2': 'value2',
            'prop3': 'value3'
        };
        var selectedProperties = ['prop1', 'prop2'];
        var str = JSON.stringify(obj, selectedProperties);
        // str
        // {"prop1":"value1","prop2":"value2"}
        
        function selectedProperties(key, val) {
            // the first val will be the entire object, key is empty string
            if (!key) {
                return val;
            }
            if (key === 'prop1' || key === 'prop2') {
                return val;
            }
            return;
        }

        var str = JSON.stringify(obj, selectedProperties, '\t\t');
        /* str output with double tabs in every line.
        {
                "prop1": "value1",
                "prop2": "value2"
        }
        */

- 16/2/8 Advanced Javascript Properties(16/2/9)

        Object.defineProperty(dest, propName, options)
        
        Object.defineProperties(dest, {
          propA: optionsA,
          propB: optionsB, //...
        })
        
        function Foobar () {
          var _foo; //  true private property
        
          Object.defineProperty(obj, 'foo', {
            get: function () { return _foo; }
            set: function (value) { _foo = value }
          });
        }
        var foobar = new Foobar();
        foobar.foo; // 15
        foobar.foo = 20; // _foo = 20

- 16/2/7 Flattening multidimensional Arrays in JavaScript(16/2/8)
    
    Solution 1: Using concat() and apply()
    
        var myNewArray = [].concat.apply([], myArray);
        // [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    Solution 2: Using reduce()
    
        var myNewArray = myArray.reduce(function(prev, curr) {
          return prev.concat(curr);
        });
        // [1, 2, 3, 4, 5, 6, 7, 8, 9]
    
    Solution 3:
    
        var myNewArray3 = [];
        for (var i = 0; i < myArray.length; ++i) {
          for (var j = 0; j < myArray[i].length; ++j)
            myNewArray3.push(myArray[i][j]);
        }
        console.log(myNewArray3);
        // [1, 2, 3, 4, 5, 6, 7, 8, 9]

- 16/2/6 Deduplicate an Array(16/2/7)

    Primitives
    
        var deduped = [ 1, 1, 'a', 'a' ].filter(function (el, i, arr) {
            return arr.indexOf(el) === i;
        });
        console.log(deduped); // [ 1, 'a' ]
    
        var deduped = [ 1, 1, 'a', 'a' ].filter( (el, i, arr) => arr.indexOf(el) === i);
        console.log(deduped); // [ 1, 'a' ]
        
        var deduped = Array.from( new Set([ 1, 1, 'a', 'a' ]) );
        console.log(deduped); // [ 1, 'a' ]
    
    Objects
    
    We can't use the same approach when the elements are Objects, because Objects are stored by reference and primitives are stored by value.
    
        1 === 1 // true
    
        'a' === 'a' // true
    
        { a: 1 } === { a: 1 } // false
    
        function dedup(arr) {
            var hashTable = {};
        
            return arr.filter(function (el) {
                var key = JSON.stringify(el);
                var match = Boolean(hashTable[key]);
        
                return (match ? false : hashTable[key] = true);
            });
        }
        
        var deduped = dedup([
            { a: 1 },
            { a: 1 },
            [ 1, 2 ],
            [ 1, 2 ],
            1,
            1,
            '1',
            '1'
        ]);
        
        console.log(deduped); // [ {a: 1}, [1, 2], 1, '1' ]

- 16/2/5 Observe DOM changes in extensions(16/2/6)

    MutationObserver is a solution to listen DOM changes and do what you want to do with elements when they changed. In following example there is some emulation of dynamic content loading with help of timers, after first "target" element creation goes "subTarget". In extension code firstly rootObserver works till targetElement appearance then elementObserver starts. This cascading observing helps finally get moment when subTargetElement found. This useful to develop extensions to complex sites with dynamic content loading.
    
        const observeConfig = {
            attributes: true,
            childList: true,
            characterData: true,
            subtree: true
        };
        
        function initExtension(rootElement, targetSelector, subTargetSelector) {
            var rootObserver = new MutationObserver(function(mutations) {
                console.log("Inside root observer");
                targetElement = rootElement.querySelector(targetSelector);
                if (targetElement) {
                    rootObserver.disconnect();
                    var elementObserver = new MutationObserver(function(mutations) {
                        console.log("Inside element observer")
                        subTargetElement = targetElement.querySelector(subTargetSelector);
                        if (subTargetElement) {
                            elementObserver.disconnect();
                            console.log("subTargetElement found!")
                        }
                    })
                    elementObserver.observe(targetElement, observeConfig);
                }
            })
            rootObserver.observe(rootElement, observeConfig);
        }
        
        (function() {
        
            initExtension(document.body, "div.target", "div.subtarget")
        
            setTimeout(function() {
                del = document.createElement("div");
                del.innerHTML = "<div class='target'>target</div>"
                document.body.appendChild(del)
            }, 3000);
    
    
        setTimeout(function() {
            var el = document.body.querySelector('div.target')
            if (el) {
                del = document.createElement("div");
                del.innerHTML = "<div class='subtarget'>subtarget</div>"
                el.appendChild(del)
            }
        }, 5000);
    
    })()

- 16/2/4 Assignment Operators(16/2/5)

    If-else (Using ternary operator)

    This is what we write on regular basis.
    
        var newValue;
        if(value > 10) 
          newValue = 5;
        else
          newValue = 2;
    We can user ternary operator to make it awesome:
    
        var newValue = (value > 10) ? 5 : 2;
        
    Null, Undefined, Empty Checks
    
        if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
             var variable2 = variable1;
        }
        
    Shorthand here:
    
        var variable2 = variable1  || '';
        
    P.S.: If variable1 is a number, then first check if it is 0.
    
    Object Array Notation
    
    Instead of using:
    
        var a = new Array();
        a[0] = "myString1";
        a[1] = "myString2";
        
    Use this:
    
        var a = ["myString1", "myString2"];
    
    Associative array
    
    Instead of using:
    
        var skillSet = new Array();
        skillSet['Document language'] = 'HTML5';
        skillSet['Styling language'] = 'CSS3';
    
    Use this:
    
        var skillSet = {
            'Document language' : 'HTML5', 
            'Styling language' : 'CSS3'
        };

- 16/2/3 Implementing asynchronous loop(16/2/4)

    Let's try out writing an asynchronous function which prints the value of the loop index every second.
    
        for (var i=0; i<5; i++) {
            setTimeout(function(){
                console.log(i);
            }, 1000);
        }  
    The output of the above programs turns out to be
    
        > 5
        > 5
        > 5
        > 5
        > 5
    
    Reason
    
    Each timeout refers to the `original i`, not a copy. So the for loop increments i until it gets to 5, then the timeouts run and use the current value of i (which is 5).
    
    An immediate solution that strikes is to cache the loop index in a temporary variable.
    
        for (var i=0; i<5; i++) {
            var temp = i;
            setTimeout(function(){
                console.log(temp);
            }, 1000);
        }  
    But again the output of the above programs turns out to be
    
        > 5
        > 5
        > 5
        > 5
        > 5
    So, that doesn't work either, because blocks don't create a scope and variables initializers are hoisted to the top of the scope. In fact, the previous block is the same as:
    
        var temp;
        for (var i=0; i<5; i++) {
            temp = i;
            setTimeout(function(){
                console.log(i);
            }, 1000);
        }  
    
    Solution
    
        for (var i=0; i<5; i++) {
            (function(num){
                setTimeout(function(){
                    console.log(num);
                }, 1000);
            })(i);
        }  
    
    In JavaScript, arguments are passed by value to a function. So primitive types like numbers, dates, and strings are basically copied. If you change them inside the function, it does not affect the outside scope. Objects are special: if the inside function changes a property, the change is reflected in all scopes.

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
        
- 16/1/26 Filtering and Sorting a List of Strings(16/2/3)

    You may have a big list of names you need to filter in order to remove duplicates and sort them alphabetically.
    
        var filteredAndSortedKeywords = keywords
          .filter(function (keyword, index) {
              return keywords.indexOf(keyword) === index;
            })
          .sort(function (a, b) {
              if (a < b) return -1;
              else if (a > b) return 1;
              return 0;
            });
        
        const filteredAndSortedKeywords = keywords
          .filter((keyword, index) => keywords.indexOf(keyword) === index)
          .sort((a, b) => {
              if (a < b) return -1;
              else if (a > b) return 1;
              return 0;
            });

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
