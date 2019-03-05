# Graph

##Implementation

###Adjacency matrix implementations

$n \times n$ matrix of {0,1} if unlabeled or {labels} if edges are labeled; undirected matrices are symmetric.

- Wastes space for sparse edges -> using sparse matrix.
- Fast to access arbitrary node's edges.

###Adjacency list implementations

List of edge lists for nodes.

- Fast arbitrary node access for numbered nodes, space efficient.

###Connected nodes implementation

- Most common implementation due to nice mapping to objects.
- Each node has info about node and edge list.
- Use list or dictionary index if you need to access nodes directly.

```python
class Node:
  def __init__(self, value):
    self.value = value
    self.edges = [] # outgoing edges
  def add(self, target:Node):
    self.edges.append(target)
```

##### Implementation with labels

```python
class LNode:
    def __init__(self, value):
        self.value = value
        self.edges = {}
	def add(self, label, target):
        self.edges[label] = target
```

## Search

###Depth-first Search

Visits all reachable nodes from p, avoiding cycles.

```python
def walk_graph(p:Node, visited=set()):
    if p in vistited: return
    visited.add(p)
    for q in p.edges:
        walk_graph(q, visited)
```

For $n$ nodes, $m$ edges, $m$ can be $n^2$:

$O(n,m) = n+m$