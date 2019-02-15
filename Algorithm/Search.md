# 1.2. Searching

## Data Structure

### Binary Tree

$T(n) = k+2T(\frac{n}{2})​$

```python
def search_tree(p:TreeNode, x:object) -> TreeNode:
	if p is None: return None
    if x==p.value: return p
    q = search_tree(p.left, x)
    if q is not None: return q
    return search_tree(p.right, x)
```

### Binary Search Tree

$T(n) = k+T(\frac{n}{2})$

```python
def search(p:TreeNode, x:object) -> TreeNode:
    if p is None: return None
    if x<p.value:
        return search(p.left, x)
    elif x>p.value:
        return search(p.right, x)
    # x == p.value
    return p
```
