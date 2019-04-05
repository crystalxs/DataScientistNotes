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

###Depth-first Search Walk 

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

