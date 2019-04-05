# Function

>A sequence of operations grouped into a single, named entity is called a **function**. Functions are like mini programs or subprograms that we can plan out just like full programs.

## Function Template

```python
def funcname(argname):
    statement 1
    statement 2
    ...
    return expression
```

* **Invoking a function** with arguments looks like *funcname*(*expression*) or *funcname*(*expression1*, *expression2*) etc... The order of the arguments matters. Python matches the first expression with the first argument name given in the function definition.

##Visibility of Symbols

**Global Variables:** variables created outside of a function, because they live in the global space (or frame).

**Local Variables:**

**Parameters:**

* Main programs cannot see variables and arguments inside functions; just because a main program can call a function, doesn't mean it can see the inner workings. Think of functions as black boxes that take parameters and return values.
* Functions can technically see global variables but don't do this as a general rule. Pass the global variables that you need to each function as arguments.