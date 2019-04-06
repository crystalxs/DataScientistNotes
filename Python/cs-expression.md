# Expression

An *expression* is a combination of values, variables, and operators. A value all by itself is considered an expression, and so is a variable.

##Order of operation

Python follows mathematical convention. The acronym *PEMDAS* is a useful way to remember the rules:

- **Parentheses** have the highest precedence and can be used to force an expression to evaluate in the order you want.
- **Exponentiation** has the next highest precedence.
- **Multiplication** and **Division** have the same precedence, which is higher than **Addition** and **Subtraction**, which also have the same precedence.
- Operators with the same precedence are evaluated from left to right.

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

