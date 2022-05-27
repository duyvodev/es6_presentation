## *Arrow Function* :bow_and_arrow:
---
- #### Definition :astonished:
    *Arrow functions allows a short syntax for writing function expressions.*
- #### Advantages :+1:
  1. Short syntax
  2. You don't need the `function` keyword, the `return` keyword, and the curly brackets `{}`.
  ***Example:***
        ```javascript
            // ES5
            var x = function(x, y) {
            return x * y;
            }
            
            // ES6
            const x = (x, y) => x * y;
        ```
- #### Disadvantages :-1:
  1. Using `const` is safer than using `var`, because a function expression is always a constant value
   ***Example:***
        ```javascript
            let log2 = (msg) => {
                console.log(msg)
            }

            log2("hello") // hello

            log2 = 2

            log2() //Uncaught TypeError: log2 is not a function
        ```
    2. Arrow functions do not have their own `this`. They are not well suited for defining object methods.

        ***Example:***
        ```javascript
            // Regular function
            let obj = {
                name: "Duy",
                age: 22,
                talk: function() {
                    console.log(this.name + " " + this.age);
                }
            }

            obj.talk() // Duy 22    
        ```
        ```javascript
            // Arrow function
            let obj = {
                name: "Duy",
                age: 22,
                talk: () => {
                    console.log(this.name + " " + this.age);
                }
            }

            obj.talk() // undefined  
        ```
        ```javascript
            // Arrow function with window properties inside context declaration 
            let obj = {
                name: "Duy",
                age: 22,
                talk: () => {
                    console.log(this.name + " " + this.age);
                }
            }
            var name = "window"
            var age = 9999

            obj.talk() // window 9999
        ```
        ```javascript
            // Arrow function with window properties global declaration 
            let obj = {
                name: "Duy",
                age: 22,
                talk: () => {
                    console.log(this.name + " " + this.age);
                }
            }
            var name = "window"
            var age = 9999

            obj.talk() // window 9999
        ```
  3. Arrow functions are not hoisted. They must be defined **before** they are used.
    ***Example:***
        ```javascript
            // Regular function with hoisting
            log3("hello") //hello
            function log3(msg){
                console.log(msg)
            }

            // Arrow function without hoisting
            log4("hello") //Uncaught ReferenceError: log4 is not defined
            const log3 = (msg) => {
                console.log(msg)
            }  
        ```
  4. Arrow functions don't have `arguments` obj
    ***Example:***
        ```javascript
            function log4(){
                console.log(arguments)
            }

            log4(1,2,3,4,5) //Arguments(5) [1, 2, 3, 4, 5, callee: ƒ, Symbol(Symbol.iterator): ƒ]

            const log5 = () => {
                console.log(arguments)
            }

            log5(1,2,3,4,5) // Uncaught ReferenceError: arguments is not defined
        ```
## *For/of loop* ➿
---
- #### Definition :astonished:
    *The JavaScript* `for/of` *statement loops through the values of an iterable objects.*
    `for/of` *lets you loop over data structures that are iterable such as Arrays, Strings, Maps, NodeLists, and more...*
- #### Advantages :+1:
    1. Short syntax
    ***Example:***
        ```javascript
            //Regular for loop
            for (let i = 0; i <= arr.length; i++) {
                console.log(arr[i])
            }

            //For/of loop
            for (let i of arr) {
                console.log(i)
            }
        ```
- #### Disadvantages :-1:
    1. `for/of` loops take more time than `regular for` loops
    ***Example:***
        ```javascript
            var arr = [];
            for (let i = 0; i <= 10000; i++) {
            arr.push(i);
            }
            
            console.time("regular for loop");
            for (let i = 0; i <= arr.length; i++) {}
            console.timeEnd("regular for loop");
            // regular for loop: 0.595947265625 ms

            console.time("for in loop");
            for (let i in arr) {}
            console.timeEnd("for in loop");
            // for in loop: 2.30517578125 ms

            console.time("for of loop");
            for (let i of arr) {}
            console.timeEnd("for of loop");
            // for of loop: 2.427978515625 ms
        ```