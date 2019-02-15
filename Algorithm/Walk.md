# 1.1. Walking Data Structure

## Array

* Arrays provide super fast random-access to the `i`th element.
* Incrementing / decrementing a pointer or index is most common walk.

##### Matrix

* 2D arrays, random-access to `i,j`.

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



##Linked list

* Linked list doesn't have random-access to `i`th element.
* From linked list we can look forward or backward.

### While Loop with Pointer

```python
p = head
while p is not None:
    print(p.value)
    p = p.next
```

##Trees

### Binary Tree

####Preorder

Compute before visiting nodes

```python
def walk_tree(p:TreeNode):
    if p is None: return
    print(p.value)
    walk_tree(p.left)
    walk_tree(p.right)
```

#### Postorder

Compute after visiting nodes

```python
def walk_tree(p:TreeNode):
	if p is None: return
    walk_tree(p.left)
    walk_tree(p.right)
    print(p.value)
```

##Graph

```python
def walk_graph(p:graphNode):
    if p is None: return
    print(p.value)
    for q in p.edges:
        walk_graph(q)

```

