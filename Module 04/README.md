### Module 04:
- #### Variable scope
    - Different Scopes
        - Javascript has 3 different scopes : Global Scope, Function Scope and Block Scope
            - Block Scope
                ```js
                    //Block Scope is set with {}
                    {
                        var a=2;
                        let b=2;
                    }
                    // var variables cannot have Block scope but let variables can.
                    // a is accessible here but not b.
            - Function Scope:
                ```js
                    //var, let and const have functional scope
                    function foo(){
                        var a=2;
                        let b=3;
                        const c=4;
                    }
                    // a, b and c are not accesible outside of the function
                ```
            - Global Javascript Variable:
                ```js
                    //A variable declared outside any block become Global
                    var a=2;
                    let b=3;
                    const c=4;
                ```
- #### var, const, let
    - var
        - var can have functional scope and global scope.
        ```js
            function foo(){
                {
                    var a=2;
                }
                //a is still accessible here
                console.log(a); //2
            }
            //a is not accesible outside of the function
            console.log(a); //undefined
    - let - const
        - let can have functional scope, global scope and block scope.
        ```js
            function foo(){
                {
                    let b=2;
                    const c=3;
                }
                //b and c are not accessible outside of the block
                console.log(b, c); //undefined
                let b=2;
                const c=3;
                //The variables a and c can be declared out of the block
                console.log(b, c); 
            }
            //Out of the function the variables b and c are undefined as well.
        ```
- #### Hoisting
    - var
        - A variable "var" can be used before it has been declared.
        ```js
            //using var before to declare it.
            b=2;
            console.log(b)//2
            var b;
        ```
        Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope
    - let, const
        - let and const are hoisting as well but not initialized until the variable is declared. (The time between the start and the variable declaration is known as Tempral Dead Zone, the variable exist but cannot be used.)
        ```js
            b=2;
            c=3
            console.log(b);//Reference error
            console.log(c);
            let b;
            const c;
        ```
    - Only declarations are hoisted
        - Javascript only hoisted only the declaration and not the initialization, if you want to use hoisted you will need to initialize the variable before to use it.
        ```js
            console.log(a); //undefined
            var a=5;
        ```

- #### Closures
- #### Hidden variables
- #### Lexical environment
- #### Nested functions
- #### Code blocks
- #### Overriding outer variables

