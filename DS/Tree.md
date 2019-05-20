# Tree

##Binary tree

A tree with exactly two sub-trees for each node, called the `left` and `right` sub-trees.

```python
class TreeNode:
    def __init__(self, value, left, right):
        self.value = value
        self.left = left
        self.right = right
```

###Depth-first Walk 

**Preorder**: Compute before visiting nodes

**Inorder:** Compute between visiting left node and right node

**Postorder**: Compute after visiting nodes

#### Recursion

```python
def dfs(p:TreeNode):
    if p is None: return
    print(p.value)
    dfs(p.left)
    dfs(p.right)
```

#### Iteration

```python
def dfs(p:TreeNode):
  	stack = []
    while p or len(stack)!=0:
      	while p:
          	stack.append(p)
            p = p.left
        p = stack.pop()
        p = p.right
```

###Breadth-first Walk

```python
def walk(t:TreeNode) -> int:
    if t is None: return 0
    return t.value + walk(t.left) + walk(t.right)
```

##Binary Search Tree

A binary tree where, for each node `m`, the left sub-tree only has nodes with keys smaller than (according to some total order) the key of `m`, while the right sub-tree only has nodes with keys larger than the key of `m`.

```python
def search_tree(p:TreeNode, value) -> None:
    "add nodes like a binary search tree"
    if value < p.value:
        if p.left is not None: add(p.left, value)
        else: p.left = TreeNode(value)
    if value > p.value:
        if p.right is not None: add(p.right, value)
        else: p.right = TreeNode(value)
    # do nothing if equal (already there)
```

### Restricted Walk

```python
def walk_search_tree(p:TreeNode, x:object):
    if p is None: return None
    if x<p.value:
        return walk_search_tree(p.left, x)
    if x>p.value:
        return walk_search_tree(p.right, x)
    return p
```

## Balanced Binary Tree

A binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

## Complete Binary Tree

> Each level has all of its nodes;
>
> The exception to this is the bottom level of the tree, which we fill in from left to right.



## Binary Heap

> When we diagram the heap it looks a lot like a tree, but when we implement it we use only a single list as an internal representation.

### Operations

- `BinaryHeap()` creates a new, empty, binary heap.
- `insert(k)` adds a new item to the heap.
- `findMin()` returns the item with the minimum key value, leaving item in the heap.
- `delMin()` returns the item with the minimum key value, removing the item from the heap.
- `isEmpty()` returns true if the heap is empty, false otherwise.
- `size()` returns the number of items in the heap.
- `buildHeap(list)` builds a new heap from a list of keys.

## Min Heap

> The smallest key is always at the front.

## Max Heap

> The largest key value is always at the front.