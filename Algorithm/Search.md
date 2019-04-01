# Searching

## Binary Search

If we know data is sorted, split recursively in half.

```python
def binsearch(a, x):
    left = 0
    right = len(a)-1
    while left<=right:
        mid = int((left+right)/2)
        if a[mid]==x:
            return mid
        elif x<a[mid]:
            right = mid-1
        else:
            left = mid+1
    return -1
```

##### Recursive Version

```python
def binsearch(a, x, left, right):
    print(left, right)
    if left>right: return -1
    mid = int((left+right)/2)
    if a[mid]==x:
        return mid
    elif x<a[mid]:
        return binsearch(a,x,left,mid-1)
    else:
        return binsearch(a,x,mid+1,right)
```

## Binary Search Tree

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

### Binary Tree

$T(n) = k+2T(\frac{n}{2})$

```python
def search_tree(p:TreeNode, x:object) -> TreeNode:
	if p is None: return None
    if x==p.value: return p
    q = search_tree(p.left, x)
    if q is not None: return q
    return search_tree(p.right, x)
```

## Hash Search

### Rabin-Karp

```python
def seach(doc, s) -> int:
    n = len(doc)
    m = len(s)
    hs = hash(s)
    for i in range(0, n-m+1):
        hdoc = hash(doc[i:i+m])
        if hdoc==hs and s==doc[i:i+m]:
                return i
    return -1

def hash(s:str) -> int:
    return sum(ord(c) for c in s)
```

Worst-case: $O(nm)$

### Improved

```python
def hash(s:str, n) -> int:
    retrun sum(ord(s[i]) for i in range(n))
    
def search(doc, s) -> int:
    n = len(doc)
    m = len(s)
    hs = hash(s, m)
    hdoc = hash(doc, m)
    for i in range(0, n-m+1):
        if hdoc==hs and s==doc[i:i+m]:
            return i
        next = ord(doc[i+m]) if i+m<n else 0
        hdoc = hdoc - ord(doc[i]) + next
    return -1
```

### Revisit Recursive Bucket sort

For $n=len(doc), m=len(s)$: $T(n,m)=m$

### TRIE or Prefix Trees

```python
class TrieNode:
    def __init__(self):
        self.edges = {}

def add(p:TrieNode, s:str, i=0) -> Node:
    if i>=len(s): return
    if s[i] not in p.edges:
        p.edges[s[i]] = TrieNode()
    add(p.edges[s[i]], s, i+1)
    
def search(root:TrieNode, s:str, i=0) -> bool:
    p = root
    while p is not None:
        if i>=len(s): return True
        if s[i] not in p.edges: return False
        p = p.edges[s[i]]
        i += 1
    return True
```

