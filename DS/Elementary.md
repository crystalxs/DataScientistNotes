# 0.0 Elementary Data Structure

Data structures group or encode relationships between data elements.

#### Advice

- Using the simplest data structure you can initially
- Wasting processor, memory power before brianpower
- There is a trade off between time and space (always)
- Prep work or more sophisticated data structure can help (???)

## Methods

- Physical adjacency or relative position in RAM
- Pointers

## Type

| Abstract data type | Implementation data type |
| ------------------ | ------------------------ |
| list               | array                    |
| dictionary         | hashtable                |
|                    |                          |

### Elemental data in memory

- int, float, string
- np.float32, np.float64
- 

### Linked List

```python
class LLNode:
	def __init__(self, value, next=None):
		self.value = value
		self.next = next
```

### Set

### Queue

### Stack

### Dictionary

### Trees

####Binary tree

```
class TreeNode:
    def __init__(self, value, left, right):
        self.value = value
        self.left = left
        self.right = right
```

#### Binary Search Tree

```python
class TreeNode:
    def __init__(self, value, left, right):
        self.value = value
        self.left = left
        self.right = right
        
def add(p:TreeNode, value) -> None:
    "add nodes like a binary search tree"
    if value < p.value:
        if p.left is not None: add(p.left, value)
        else: p.left = TreeNode(value)
    if value > p.value:
        if p.right is not None: add(p.right, value)
        else: p.right = TreeNode(value)
    # do nothing if equal (already there)
```

### Graph

```python
class Node:
  def __init__(self, value):
    self.value = value
    self.edges = [] # outgoing edges
  def add(self, target):
    self.edges.append(target)
```



