# Elementary Data Structure

> Reference:
>
> * http://bigocheatsheet.com/
>
> * https://www.cnblogs.com/gaochundong/p/data_structures_and_asymptotic_analysis.html

##Array

- Array implementations is most common for list abstract data structure;
- Lists are ordered but items aren't necessarily sortable;
- Arrays use contiguous memory locations to associate items.

#### Complexity

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

##Matrix

- 2D arrays, random-access to `i,j`.

#### Python

`table` in python; if all element are all numbers, then `matrix` in python.

####Walk

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

##Set

* unique and unordered list;
* typical implementation is a hash table;

#### Python

`set` in python.

#### Operations

add, delete, contains, union, intersection

contains: take constant time for hash table implementation

##Queue

* Ordered list restricted to add to the end and delete from the front;

* First in first out, last in last out, **FIFO**;
* BFS implement data structure.

#### Time Complexity

Push (Insert to end): `O(1)`

Pop (Delete from begin): `O(1)`

Access: End - `O(1)`; Other - `O(n)`

#### Implementation

```python
class Queue:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def enqueue(self, item):
        self.items.insert(0,item)

    def dequeue(self):
        return self.items.pop()

    def size(self):
        return len(self.items)
```

#### Operations

| **Queue Operation** | **Queue Contents**   | **Return Value** |
| :------------------ | :------------------- | :--------------- |
| `q.isEmpty()`       | `[]`                 | `True`           |
| `q.enqueue(4)`      | `[4]`                |                  |
| `q.enqueue('dog')`  | `['dog',4]`          |                  |
| `q.enqueue(True)`   | `[True,'dog',4]`     |                  |
| `q.size()`          | `[True,'dog',4]`     | `3`              |
| `q.isEmpty()`       | `[True,'dog',4]`     | `False`          |
| `q.enqueue(8.4)`    | `[8.4,True,'dog',4]` |                  |
| `q.dequeue()`       | `[8.4,True,'dog']`   | `4`              |
| `q.dequeue()`       | `[8.4,True]`         | `'dog'`          |
| `q.size()`          | `[8.4,True]`         | `2`              |

##Stack

* Ordered list restricted to add to the end and delete from the end;
* First in last out, last in first out, **FILO**;
* DFS implement data structure.

#### Time Complexity

Push (Insert to end): `O(1)`

Pop (Delete from end): `O(1)`

Access: End - `O(1)`; Other - `O(n)`

#### Implementation

```python
class Stack:
     def __init__(self):
         self.items = []

     def isEmpty(self):
         return self.items == []

     def push(self, item):
         self.items.append(item)

     def pop(self):
         return self.items.pop()

     def peek(self):
         return self.items[len(self.items)-1]

     def size(self):
         return len(self.items)
```

#### Operations

| **Stack Operation** | **Stack Contents**   | **Return Value** |
| :------------------ | :------------------- | :--------------- |
| `s.isEmpty()`       | `[]`                 | `True`           |
| `s.push(4)`         | `[4]`                |                  |
| `s.push('dog')`     | `[4,'dog']`          |                  |
| `s.peek()`          | `[4,'dog']`          | `'dog'`          |
| `s.push(True)`      | `[4,'dog',True]`     |                  |
| `s.size()`          | `[4,'dog',True]`     | `3`              |
| `s.isEmpty()`       | `[4,'dog',True]`     | `False`          |
| `s.push(8.4)`       | `[4,'dog',True,8.4]` |                  |
| `s.pop()`           | `[4,'dog',True]`     | `8.4`            |
| `s.pop()`           | `[4,'dog']`          | `True`           |
| `s.size()`          | `[4,'dog']`          | `2`              |

## Deque

known as a double-ended queue, is an ordered collection of items similar to the queue. It has two ends, a front and a rear, and the items remain positioned in the collection. 

#### Implementation

```python
class Deque:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def addFront(self, item):
        self.items.append(item)

    def addRear(self, item):
        self.items.insert(0,item)

    def removeFront(self):
        return self.items.pop()

    def removeRear(self):
        return self.items.pop(0)

    def size(self):
        return len(self.items)
```

#### Operations

| **Deque Operation** | **Deque Contents**         | **Return Value** |
| :------------------ | :------------------------- | :--------------- |
| `d.isEmpty()`       | `[]`                       | `True`           |
| `d.addRear(4)`      | `[4]`                      |                  |
| `d.addRear('dog')`  | `['dog',4,]`               |                  |
| `d.addFront('cat')` | `['dog',4,'cat']`          |                  |
| `d.addFront(True)`  | `['dog',4,'cat',True]`     |                  |
| `d.size()`          | `['dog',4,'cat',True]`     | `4`              |
| `d.isEmpty()`       | `['dog',4,'cat',True]`     | `False`          |
| `d.addRear(8.4)`    | `[8.4,'dog',4,'cat',True]` |                  |
| `d.removeRear()`    | `['dog',4,'cat',True]`     | `8.4`            |
| `d.removeFront()`   | `['dog',4,'cat']`          | `True`           |

## Linked List

- Non-contiguous lists;
- Implement with explicit pointers from one element to the next.
- Linked list doesn't have random-access to `i`th element.
- From linked list we can look forward or backward.

#### Time Complexity

Access: begin - `O(1)`; end - `O(n)`

Insert: `O(1)`

Delete: `O(1)`

#### Implementation

```python
class LLNode:
	def __init__(self, value, next=None):
		self.value = value
		self.next = next
```

- `head = LLNode('')`, `head` is a pointer

#### Walk while Loop with Pointer

```python
p = head		# cursor
while p is not None:
    print(p.value)
    p = p.next
```

#### Insertion at head

```python
x = LLNode('mary')
x.next = head
head = x
```

#### Deletion of node

```python
delete = head.next				# node to be deleted
before_delete.next = delete.next
```

## Dictionary

Arrange two lists side-by-side and kind of glue them together, map one value to another.

####Time Complexity

| operation     | Big-O Efficiency |
| :------------ | :--------------- |
| copy          | O(n)             |
| get item      | O(1)             |
| set item      | O(1)             |
| delete item   | O(1)             |
| contains (in) | O(1)             |
| iteration     | O(n)             |

#### Python

`dict` in python.

##Hash Table

Array of linked lists / buckets and a hash code function.

1. Compute hash code by **hash function**
2. Map the hash code to an index in the array, which bucket.

#### Time Complexity

Access: cannot access by index

Search: `O(1)` vs `O(n)`

* With a uniform distribution, we would expect roughly *N*/*B* associations in each bucket for *B* buckets and *N* total elements in the dictionary.
* A complexity of *N*/*B* is much better than *N* and, with sufficiently large *B*, we would say that *N*/*B* approaches 1, giving complexity *O(1)* versus *O(n)*.

Insert: `O(1)` vs `O(n)`

Delete: `O(1)` vs `O(n)`

#### Hash Function

Magic Number: 31

##### Open Hashing

##### Close Hashing

##### Rehashing

#### Hash Table

#### Hash Map

#### Hash Set

