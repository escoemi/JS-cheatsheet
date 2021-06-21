### Module 04:
- #### Variable scope
    - Different Scopes
        - Javascript has 3 different scopes : Global Scope, Function Scope and Block Scope
            - Block Scope
                ```js
                    //Block Scope is set just with {}
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
        - Javascript only hoisted the declaration and not the initialization, if you want to use hoisted you will need to initialize the variable before to use it.
        ```js
            console.log(a); //undefined
            var a=5;
        ```

- #### Closures
    - Function can take local or global variables to work on. For example:
    ```js
        //foo can take a global variable like a
        let a =2;
        function foo(){
            a++;
            console.log(a);
        }
        //or can create one inside of the fuction istead.
        function foo(){
            let b=2;
            console.log(b);
        }
    ```
    - Closure is way in that the function has access from outer scope even while runnning in a scope where those variables wouldn't be accessible. So the function create link to a variable and that link is available as long as the function is live.

    ```js
        function foo(){
            let teams=["cruz azul", "america", "pumas"];

            return function Addteam (newTeam){
                teams.push(newTeam);
                return teams;
            }
        }
        //b now is refearing to the function Addteam
        let b=foo();
        //Altough Addteam does not declare directly "teams" it has still access into it
        console.log(b("chivas")); //[ 'cruz azul', 'america', 'pumas', 'chivas' ]
        console.log(b("tigres")); //[ 'cruz azul', 'america', 'pumas', 'chivas', 'tigres' ]
        //each time foo is called, it create a new reference to a new variable "teams"
        let another=foo();
        console.log(another("real madrid")); // [ 'cruz azul', 'america', 'pumas', 'real madrid' ]
        console.log(another("barcelona")); // [ 'cruz azul', 'america', 'pumas', 'real madrid', 'barcelona' ]
- #### Hidden variables
- #### Lexical environment
    - Each time a curly bracket ({}) is created, a new lexical environment is created as well. It is used during the compilation to get what values should be taken for each variable. For example:
    ```js
        let bar="im a global variable";
        let global="global"
        function foo(){
            let bar="im a function variable";
            {
                let bar="im a block variable";
                //This time JS engine try to find bar on the block, then on the function and at the end on the global scope. Since it was found on the block first, then does not try again on the other scopes.
                console.log(bar); //im a block variable
                //This variable instead, it will be not found on the block, then will look at the function and then will find it on the global scope 
                console.log(global); //global
            }
            //JS engine try to find bar first on the function and then on the global scope.
            console.log(bar); //im a function variable
        }
        //JS engine only find the variable on the global scope.
        console.log(bar); //im a global variable
        foo();
    ```
    - So JS engine look up at the first block where it was called and so on until find the variable assigned. 
- #### Nested functions
    - A function is called nested when its created inside another function. For example:
    ```js
        function foo(countryFilter){
            let countries=["Mexico", "US", "Germany", "Japan"];
            //filter function is called inside foo function
            function filter(name){
                return countries.filter((country)=>country!==name);;
            }

            return filter(countryFilter);
        }

        console.log(foo("Mexico"));
    ```
    - Here the nested function filter() is made for convenience. It can access the outer variables and so can return the list filtered
- #### Code blocks
    - Javascript statements can be grouped togheter using codeblocks, that is, set the code inside of curly brackets ({...}). 
    - Each time a code block is created, it creates a new lexical scope. New variables will be available on the block, but not outside of that.
    ```js
        let a="defining a";
        {
            let a="redifining a";
            console.log(a);// redifining a
        }
        console.log(a); //defining a
    ```
- #### Overriding outer variables
    - Overriding outer variables or shadowing, is used when you need to maintain two or more variables of the same name. In that you must use separate scopes. For example:
    ```js
    var studentName="Suzy";

    function printStudent(studentName){
        //Altough studentName is Suzy on the global scope, it is getting shadowed or overrided 
        //by the declaration of studentName inside of the function
        studentName=studentName.toUpperCase();
        console.log(studentName);
    }

    printStudent("Frank"); //FRANK
    printStudent(studentName); //SUZY
    console.log(studentName); //Suzy
    //studentName, global scope was not modified by the assignation 
    //studentName=studentName.toUpperCase();
    //because the one that changed was studentName on the function scope.
    ```

    - Since the lexical scope is different, studentName inside function is the one that has been changed and not the one from the global scope.


