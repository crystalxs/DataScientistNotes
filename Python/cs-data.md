# Data Type

> Reference:
>
> * http://interactivepython.org/courselib/static/pythonds/Introduction/GettingStartedwithData.html
>
> * https://docs.python.org/3/tutorial/datastructures.html

##Variables / Data Alias

In Python the variable are always hold a **reference** to a piece of data and **not the data itself**.

### Shallow Copy



##Python built-in atomic data type

- Numeric: `int`, `float`;

  - Operation: `+`, `-`, `*`, `/`, `**`(exponentiation), `%`(modulo), `//`(integer division).
  - When two integers are divided, the result is a **floating** point. The integer division operator returns the integer portion of the quotient by truncating any fractional part.

- Boolean: `bool` (`True` / `False`).

  | **Operation Name**    | **Operator** | **Explanation**                                              |
  | :-------------------- | :----------- | :----------------------------------------------------------- |
  | less than             | <            | Less than operator                                           |
  | greater than          | >            | Greater than operator                                        |
  | less than or equal    | <=           | Less than or equal to operator                               |
  | greater than or equal | >=           | Greater than or equal to operator                            |
  | equal                 | ==           | Equality operator                                            |
  | not equal             | !=           | Not equal operator                                           |
  | logical and           | and          | Both operands True for result to be True                     |
  | logical or            | or           | One or the other operand is True for the result to be True   |
  | logical not           | not          | Negates the truth value, False becomes True, True becomes False |

##Python built-in collection data type

| Data Type Name | Ordered or not | Mutability |               |
| -------------- | -------------- | ---------- | ------------- |
| List           | Ordered        | Mutable    | heterogeneous |
| String         | Ordered        | Immutable  |               |
| Tuple          | Ordered        | Immutable  | heterogeneous |
| Set            | Unordered      | Mutable    | heterogeneous |
| Dictionary     | Unordered      | Mutable    |               |

### List

An ordered collection of zero or more references to Python data objects.

```python
myList = []
```

#### Operation

| **Operation Name** | **Operator** | **Explanation**                         |
| :----------------- | :----------- | :-------------------------------------- |
| indexing           | [ ]          | Access an element of a sequence         |
| concatenation      | +            | Combine sequences together              |
| repetition         | *            | Concatenate a repeated number of times  |
| membership         | in           | Ask whether an item is in a sequence    |
| length             | len          | Ask the number of items in the sequence |
| slicing            | [ : ]        | Extract a part of a sequence            |

####Method

| **Method Name** | **Use**                | **Explanation**                                       |
| :-------------- | :--------------------- | :---------------------------------------------------- |
| `append`        | `alist.append(item)`   | Adds a new item to the end of a list                  |
| `insert`        | `alist.insert(i,item)` | Inserts an item at the ith position in a list         |
| `pop`           | `alist.pop()`          | Removes and returns the last item in a list           |
| `pop`           | `alist.pop(i)`         | Removes and returns the ith item in a list            |
| `sort`          | `alist.sort()`         | Modifies a list to be sorted                          |
| `reverse`       | `alist.reverse()`      | Modifies a list to be in reverse order, **no return** |
| `del`           | `del alist[i]`         | Deletes the item in the ith position                  |
| `index`         | `alist.index(item)`    | Returns the index of the first occurrence of `item`   |
| `count`         | `alist.count(item)`    | Returns the number of occurrences of `item`           |
| `remove`        | `alist.remove(item)`   | Removes the first occurrence of `item`                |

### String

A sequential collections of zero or more letters, numbers and other symbols. We call these letters, numbers and other symbols *characters*. Literal string values are differentiated from identifiers by using quotation marks (either single or double).

#### Operation

Support all [`list` operations](#List).

####Method

| **Method Name** | **Use**                | **Explanation**                                           |
| :-------------- | :--------------------- | :-------------------------------------------------------- |
| `center`        | `astring.center(w)`    | Returns a string centered in a field of size `w`          |
| `count`         | `astring.count(item)`  | Returns the number of occurrences of `item` in the string |
| `ljust`         | `astring.ljust(w)`     | Returns a string left-justified in a field of size `w`    |
| `lower`         | `astring.lower()`      | Returns a string in all lowercase                         |
| `rjust`         | `astring.rjust(w)`     | Returns a string right-justified in a field of size `w`   |
| `find`          | `astring.find(item)`   | Returns the index of the first occurrence of `item`       |
| `split`         | `astring.split(schar)` | Splits a string into substrings at `schar`                |

- `split` will return `''` if there is nothing between two `schar`.

### Tuple

Tuples are very similar to lists in that they are heterogeneous sequences of data. The difference is that a tuple is immutable, like a string. A tuple cannot be changed. Tuples are written as comma-delimited values enclosed in parentheses.

#### Operation

Support all [`list` operations](#List).

### Set

A set is an unordered collection of zero or more immutable Python data objects. Sets do not allow duplicates and are written as comma-delimited values enclosed in curly braces.

```python
mySet = set()
mySet = {3,6,"cat",4.5,False}
```

#### Operation

| **Operation Name** | **Operator**       | **Explanation**                                              |
| :----------------- | :----------------- | :----------------------------------------------------------- |
| membership         | in                 | Set membership                                               |
| length             | len                | Returns the cardinality of the set                           |
| `|`                | `aset | otherset`  | Returns a new set with all elements from both sets           |
| `&`                | `aset & otherset`  | Returns a new set with only those elements common to both sets |
| `-`                | `aset - otherset`  | Returns a new set with all items from the first set not in second |
| `<=`               | `aset <= otherset` | Asks whether all elements of the first set are in the second |

#### Method

| **Method Name** | **Use**                       | **Explanation**                                              |
| :-------------- | :---------------------------- | :----------------------------------------------------------- |
| `union`         | `aset.union(otherset)`        | Returns a new set with all elements from both sets           |
| `intersection`  | `aset.intersection(otherset)` | Returns a new set with only those elements common to both sets |
| `difference`    | `aset.difference(otherset)`   | Returns a new set with all items from first set not in second |
| `issubset`      | `aset.issubset(otherset)`     | Asks whether all elements of one set are in the other        |
| `add`           | `aset.add(item)`              | Adds item to the set                                         |
| `remove`        | `aset.remove(item)`           | Removes item from the set                                    |
| `pop`           | `aset.pop()`                  | Removes an arbitrary element from the set                    |
| `clear`         | `aset.clear()`                | Removes all elements from the set                            |

###Dictionary

A collections of associated pairs of items where each pair consists of a key and a value. This key-value pair is typically written as key:value. Dictionaries are written as comma-delimited key:value pairs enclosed in curly braces. 

```python
myDict = {}
```

#### Operation

| **Operator** | **Use**          | **Explanation**                                              |
| :----------- | :--------------- | :----------------------------------------------------------- |
| `[]`         | `myDict[k]`      | Returns the value associated with `k`, otherwise its an error |
| `in`         | `key in adict`   | Returns `True` if key is in the dictionary, `False` otherwise |
| `del`        | del `adict[key]` | Removes the entry from the dictionary                        |

#### Method

| **Method Name** | **Use**            | **Explanation**                                              |
| :-------------- | :----------------- | :----------------------------------------------------------- |
| `keys`          | `adict.keys()`     | Returns the keys of the dictionary in a dict_keys object     |
| `values`        | `adict.values()`   | Returns the values of the dictionary in a dict_values object |
| `items`         | `adict.items()`    | Returns the key-value pairs in a dict_items object           |
| `get`           | `adict.get(k)`     | Returns the value associated with `k`, `None` otherwise      |
| `get`           | `adict.get(k,alt)` | Returns the value associated with `k`, `alt` otherwise       |