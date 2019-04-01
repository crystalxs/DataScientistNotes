# Exception Handling

There are two types of errors that typically occur when writing programs:

* **Syntax Error:** simply means that the programmer has made a mistake in the structure of a statement or expression;
* **Logic Error:** denotes a situation where the program executes but gives the wrong result.

When an exception occurs, we say that it has been “raised.” You can “handle” the exception that has been raised by using a `try` statement.

```python
try:
except:
```

It is also possible for a programmer to cause a runtime exception by using the `raise` statement. 

```python
if anumber < 0:
    raise RuntimeError("You can't use a negative number")
else:
  	print(math.sqrt(anumber))
```

