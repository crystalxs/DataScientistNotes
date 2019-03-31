# Elementary Data Structure

http://bigocheatsheet.com/

https://www.cnblogs.com/gaochundong/p/data_structures_and_asymptotic_analysis.html

##Array

- Array implementations is most common for list abstract data structure;
- Lists are ordered but items aren't necessarily sortable;
- Arrays use contiguous memory locations to associate items.

#### Complexity

Access: `O(1)`

Insert: `O(1)`

Delete: `O(1)`

Search: -

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

#### Operations

add, delete, contains, union, intersection

contains: take constant time for hash table implementation

#### Python

`set` in python.

##Queue

* Ordered list restricted to add to the end and delete from the front;

* First in first out, last in last out, **FIFO**;
* BFS implement data structure.

#### Time Complexity

Push (Insert to end): `O(1)`

Pop (Delete from begin): `O(1)`

Access: End - `O(1)`; Other - `O(n)`

##Stack

* Ordered list restricted to add to the end and delete from the end;
* First in last out, last in first out, **FILO**;
* DFS implement data structure.

#### Time Complexity

Push (Insert to end): `O(1)`

Pop (Delete from end): `O(1)`

Access: End - `O(1)`; Other - `O(n)`

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

