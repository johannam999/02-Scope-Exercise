#### Questions:
1. When this code is run in Node, e.g. `node index.js`, what are the two stages of execution for this file called, and which order do they happen in?

    First the compiler will run to identify all the variables that were assigned and will hoist them. Next step is the engine run to interpret the values of the variables that were found by compiler and execute all the functions.

2. Write an explanation, using as much space as you need, relating to how the first stage of execution for this file operates.- For example, identify the high level steps in a line by line overview and then define what each of those steps are accomplishing.
    
    
    The first stage of execution for this file will compile the global scope.  It will iterate line by line over the function and variable declarations, and also determine the value of 'this' if it is present.  
    In this case:
    on line 3, the variable `foo` is recognized and added to the scope,
    on line 5, the function `bar` is recognized and added to the scope.
    There are no other declarations outside of the bar function, so the compile stage is finished for the global scope.

3. Write an explanation, using as much space as you need, relating to how the second stage of execution for this file operates. - For example, identify the high level steps in a line by line overview and then define what each of those steps are accomplishing.

    `Foo` is assigned the value 'bar' on line 3.
    The `bar` function is called.  It will now be compiled and executed.
    The compiler sees `foo` on line 6 and adds it to the scope of bar.
    On line 8 the compiler adds the function `baz` to the `bar` function scope  and `bar` is now executed.
    The value 'baz' is assigned to `foo` on line 6.
    On line 13 `baz` is executed.
    `baz` is now compiled, and the parameter `foo` is added to the scope of `baz`.  There are no other declarations.
    In the execution of `baz`, `foo` is assigned the value 'bam' on line 10
    However, on line 11 a variable `bam` is referenced.  Because it has not been declared and we are running in strict mode, an error is thrown.


4. During the second stage of execution how many scopes have been registered by the engine?
  - Which segments of the code do they belong to?
  - Please identify any variables/refs and which scope each belongs to?

    Three scopes have been registered.
    The global scope, referring to code outside of the `bar` function.
    The scope for the `bar` function referring to code in `bar` but outside of the `baz` function.
    The scope for the `baz` function.
    Here are the variables/refs:

    1.Global scope:
      `foo` variable
      `bar` function
    2.`Bar` function scope:
      `foo` variable
      `baz` function
    3.`Baz` function scope:
      `foo` parameter


5. When line 13 invokes the `baz` function, which `foo` will be assigned a value of `bam`? More specifically, `bam` will be assigned to the `foo` in ??? scope. Give a brief description in your own words to support your conclusion.


    When the `baz` function is invoked, the value of 'bam' will be assigned to the `foo` parameter in the scope of the `baz` function (3rd scope), as that is the only `foo` in the scope of `baz`, and since there is a `foo` in that scope there is no need to look in other scopes.

6. Which scope, if any, will the variable `bam` on line 11 be registered to when the first stage of execution occurs on this file? Provide a brief description in your own words to support your conclusion.

    The variable `bam` on line 11 is not a declaration, so in the first stage of execution it is ignored and not assigned to any scope.

7. For each line, 16 through 19, what is the return value for each?

    Function `bar` on line 16 throws an error because `bam` is not declared and we are running in strict mode. So execution stops and there is no return value. Also, `foo` and `bam` on lines 17 and 18 are neither a variable declaration nor a function call. I have checked this execution on repl.it. 



