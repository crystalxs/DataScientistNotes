# Linked List

- Non-contiguous lists;
- Implement with explicit pointers from one element to the next.
- Linked list doesn't have random-access to `i`th element.
- From linked list we can look forward or backward.

### Time Complexity

Access: begin - `O(1)`; end - `O(n)`

Insert: `O(1)`

Delete: `O(1)`

### Implementation in Python

```python
class LLNode:
	def __init__(self, value, next=None):
		self.value = value
		self.next = next
  def __str__(self):
    return "(%s,%s)" % (self.value, str(self.next))
  def __repr__(self):
    return str(self)
```

- `head = LLNode('')`, `head` is a pointer

### Operations

#### Walk

##### while Loop with Pointer

```python
p = head		# cursor
while p is not None:
    print(p.value)
    p = p.next
```

##### Recursive

```python
def walk(p):
  	if p is None: return
    print(p.value)
  	walk(p.next)
    
walk(head)
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