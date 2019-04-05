# Expression

## Conditional Expression

```python
conditional_expression ::=  or_test ["if" or_test "else" expression]
expression             ::=  conditional_expression | lambda_expr
expression_nocond      ::=  or_test | lambda_expr_nocond
```



##Lambda Expression

> A shortened way to define functions inline.

Create an anonymous function using the “lambda” keyword at runtime.

Keyword : `lambda`

```text
lambda arguments: expression
```

Example:

```text
def add_2(x):
    return x+2
```

```text
add_2_lambda = lambda x: x+2
```

