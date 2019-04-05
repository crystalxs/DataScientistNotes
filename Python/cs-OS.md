# Input&Output

## String Format

* change the separator character by setting the `sep` argument;
* each `print` ends with a newline character by default. This behavior can be changed by setting the `end` argument.

### Formatted Strings

* The `%` operator is a string operator called the **format operator**.

* The left side of the expression holds the template or format string.
* The right side holds a collection of values that will be substituted into the format string. 

####Specifications

| **Character** | **Output Format**                                            |
| :------------ | :----------------------------------------------------------- |
| `d`, `i`      | Integer                                                      |
| `u`           | Unsigned integer                                             |
| `f`           | Floating point as m.ddddd                                    |
| `e`           | Floating point as m.ddddde+/-xx                              |
| `E`           | Floating point as m.dddddE+/-xx                              |
| `g`           | Use `%e` for exponents less than −4−4 or greater than +5+5, otherwise use `%f` |
| `c`           | Single character                                             |
| `s`           | String, or any Python data object that can be converted to a string by using the `str` function. |
| `%`           | Insert a literal % character                                 |

#### Modifier

| **Modifier** | **Example** | **Description**                                              |
| :----------- | :---------- | :----------------------------------------------------------- |
| number       | `%20d`      | Put the value in a field width of 20                         |
| `-`          | `%-20d`     | Put the value in a field 20 characters wide, left-justified  |
| `+`          | `%+20d`     | Put the value in a field 20 characters wide, right-justified |
| `0`          | `%020d`     | Put the value in a field 20 characters wide, fill in with leading zeros. |
| `.`          | `%20.2f`    | Put the value in a field 20 characters wide with 2 characters to the right of the decimal point. |
| `(name)`     | `%(name)d`  | Get the value from the supplied dictionary using `name` as the key. |

