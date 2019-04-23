# Sequential List

## Array

> * Array implementations is most common for list abstract data structure;
> * Lists are ordered but items aren't necessarily sortable;
> * Arrays use contiguous memory locations to associate items.

#### Complexity for python built-in `list`

| Operation        | Big-O Efficiency |
| :--------------- | :--------------- |
| index []         | O(1)             |
| index assignment | O(1)             |
| append           | O(1)             |
| pop()            | O(1)             |
| pop(i)           | O(n)             |
| insert(i,item)   | O(n)             |
| del operator     | O(n)             |
| iteration        | O(n)             |
| contains (in)    | O(n)             |
| get slice [x:y]  | O(k)             |
| del slice        | O(n)             |
| set slice        | O(n+k)           |
| reverse          | O(n)             |
| concatenate      | O(k)             |
| sort             | O(n log n)       |
| multiply         | O(nk)            |

#### Python

`list` in python; if element is immutable, then `tuple` in python.

- Arrays provide super fast random-access to the `i`th element.
- Incrementing / decrementing a pointer or index is most common walk.

## Matrix

> 2D arrays, random-access to `i,j`.

#### Python

`table(pandas)` in python;

If all element are all numbers, then `matrix(numpy)` in python.

#### Walk

```python
def walk(A):
    arow = A[0]
    n = len(arow)
    for i in range(A):
        for j in range(n):
            # process A[i][j] such as:
            print(f" {A[i][j]}", end='')
            
def walk_lower_triangle(A):
  	arow = A[0]
    n = len(arow)
    for i in range(A):
      	for j in range(i):
          	# process A[i][j]
```

## String

> A list only contains characters.

