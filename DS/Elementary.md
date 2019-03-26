# Elementary Data Structure

##Built-in

###Array

`list` in python; if element is immutable, then `tuple` in python.

- Arrays provide super fast random-access to the `i`th element.
- Incrementing / decrementing a pointer or index is most common walk.

###Matrix

`table` in python; if all element are all numbers, then `matrix` in python.

- 2D arrays, random-access to `i,j`.

```
def walk(A):
    arow = A[0]
    n = len(arow)
    for i in range(n):
        for j in range(n):
            # process A[i][j] such as:
            print(f" {A[i][j]}", end='')
        print()
```

###Set

All elements within a list are unique and unordered.



###Dictionary

Arrange two lists side-by-side and kind of glue them together, map one value to another.



##Implement

### Linked List

```python
class LLNode:
	def __init__(self, value, next=None):
		self.value = value
		self.next = next
```

- Linked list doesn't have random-access to `i`th element.
- From linked list we can look forward or backward.

####Walk while Loop with Pointer

```python
p = head
while p is not None:
    print(p.value)
    p = p.next
```

### Queue

First in first out.

### Stack

First in last out.

### 
