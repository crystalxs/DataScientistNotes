# Function

>A sequence of operations grouped into a single, named entity is called a **function**. Functions are like mini programs or subprograms that we can plan out just like full programs.

## Function Template

```python
def funcname(argname): # argname is optional
    statements
    return expression # return is optional
```

* **Invoking a function** with arguments looks like *funcname*(*expression*) or *funcname*(*expression1*, *expression2*) etc... The order of the arguments matters. Python matches the first expression with the first argument name given in the function definition.

### Fruitful function

The function yield results.

###Void function

The function perform an action but don't return a value.

* If you try to assign the result to a variable, you get a special value called `None` (`NoneType`).

## Flow of Execution

* Execution always begins at the first statement of the program. Statements are executed one at a time, in order from top to bottom.

* Function *definitions* do not alter the flow of execution of the program.
* Statements inside the function are not executed until the function is called.
* A function call is like a detour in the flow of execution. Instead of going to the next statement, the flow jumps to the body of the function, executes all the statements there, and then comes back to pick up where it left off.
* One function can call another. While in the middle of one function, the program might have to execute the statements in another function. But while executing that new function, the program might have to execute yet another function!

##Visibility of Symbols

**Global Variables:** variables created outside of a function, because they live in the global space (or frame).

**Local Variables:**

**Parameters:**

* Main programs cannot see variables and arguments inside functions; just because a main program can call a function, doesn't mean it can see the inner workings. Think of functions as black boxes that take parameters and return values.
* Functions can technically see global variables but don't do this as a general rule. Pass the global variables that you need to each function as arguments.