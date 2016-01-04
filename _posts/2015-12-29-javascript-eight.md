---
title: JavaScript best practices 阅读摘要
description: JavaScript best practices 阅读摘要
keywords: JavaScript best practices
category: javascript
---
# Call things by their name — easy, short and readable variable and function names

good variable and function names should be easy to understand and tell you what is going on — not more and not less. 

One trap to avoid is marrying values and functionality in names. A function called isLegalDrinkingAge() makes more sense than isOverEighteen() as the legal drinking age varies from country to country, and there are other things than drinking to consider that are limited by age.

Hungarian notation. For example, if you have a variable called familyName and it is supposed to be a string, you would write it as sFamilyName in “Hungarian”.

Keeping to English is a good idea, too.

See your code as a narrative. If you can read line by line and understand what is going on, well done. If you need to use a sketchpad to keep up with the flow of logic, then your code needs some work.

# Avoid globals

Global variables and function names are an incredibly bad idea. The reason is that every JavaScript file included in the page runs in the same scope. If you have global variables or functions in your code, scripts included after yours that contain the same variable and function names will overwrite your variables/functions.

workarounds to avoid using globals:

- return pointers ,a public alias

        myNameSpace = function(){
          var current = null;
          function init(){...}
          function change(){...}
          function verify(){...}
          return{
            init:init,
            set:change
          }
        }();

- If you don’t need any of your variables or functions to be available to the outside, simply wrap the whole construct in another set of parentheses to execute it without assigning any name to it:
    
        (function(){
          var current = null;
          function init(){...}
          function change(){...}
          function verify(){...}
        })();

# Stick to a strict coding style

Clean and valid code

# Comment as much as needed but not more

- Again the trick is moderation. Comment when there is an important thing to say, and if you do comment use the /* */ notation. Single line comments using // can be problematic if people minify your code without stripping comments and in general are less versatile.

- If you comment out parts of your code to be used at a later stage or to debug code there is a pretty sweet trick you can do:

    Adding a double slash before the closing star-slash sets your code up so that you can comment and uncomment the whole block by simply adding or removing a slash before the opening slash-star:
    
        module = function(){
          var current = null;
          function init(){
          };
        /*
          function show(){
            current = 1;
          };
          function hide(){
            show();
          };
        // */
          return{init:init,show:show,current:current}
        }();
    
    With the code set up as shown in the above block, adding a slash before the opening slash-star will turn the multiline comment into two one-line comments, “unhiding” the code in between and causing it to be executed. Removing the slash will comment it out again.

- For larger applications comment documentation in JavaDoc style makes a lot of sense — you are seeding the overall documentation of your product by writing code.


# Avoid mixing with other technologies

By adding a class called “error” to the element when there is an error, you can ensure that the styling information is kept inside the CSS, which is more appropriate:

    var f = document.getElementById('mainform');
    var inputs = f.getElementsByTagName('input');
    for(var i=0,j=inputs.length;i<j;i++){
      if(inputs[i].className === 'mandatory' &&
         inputs[i].value === ''){
        inputs[i].className += ' error';
      }
    }

# Use shortcut notation when it makes sense

- using an object literal
- using the [] array shortcut
- using “ternary notation”. `var direction = (x > 100) ? 1 : -1;`
- providing a preset value for a variable if it is not defined `var x = v || 10; `

# Modularize — one function per task

- This is a general programming best practice — making sure that you create functions that fulfill one job at a time makes it easy for other developers to debug and change your code without having to scan through all the code to work out what code block performs what function.
- This also applies to creating helper functions for common tasks. If you find yourself doing the same thing in several different functions then it is a good idea to create a more generic helper function instead, and reuse that functionality where it is needed.
- By having all your functions only perform one task you can have a main init() function for your application that contains all the application structure. That way you can easily change the application and remove functionality without having to scan the rest of the document for dependencies.

# Enhance progressively

- In essence what you should do is write code that works regardless of available technology. In the case of JavaScript, this means that when scripting is not available (say on a BlackBerry, or because of an over-zealous security policy) your web products should still allow users to reach a certain goal, not block them because of the lack of JavaScript which they can’t turn on, or don’t want to.
- It is amazing how many times you will build a massively convoluted JavaScript solution for a problem that can be solved easily without it. 

# Allow for configuration and translation

- One of the most successful tips to keep your code maintainable and clean is to create a configuration object that contains all the things that are likely to change over time. These include any text used in elements you create (including button values and alternative text for images), CSS class and ID names and general parameters of the interface you build.

# Avoid heavy nesting

- 
