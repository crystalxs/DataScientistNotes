# Tree

##Binary tree

```
class TreeNode:
    def __init__(self, value, left, right):
        self.value = value
        self.left = left
        self.right = right
```

###Depth-first Search Walk 

**Preorder**: Compute before visiting nodes

```python
def walk_tree(p:TreeNode):
    if p is None: return
    print(p.value)
    walk_tree(p.left)
    walk_tree(p.right)
```

**Postorder**: Compute after visiting nodes

```python
def walk_tree(p:TreeNode):
	if p is None: return
    walk_tree(p.left)
    walk_tree(p.right)
    print(p.value)
```

##Binary Search Tree

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

