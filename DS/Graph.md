# Graph

* A collection of connected element pairs
* The aggregate of nodes

**Nodes / vertices** connected with **edges**, which can have **labels**.

Directed graph have arrows as edges; undirected graph use lines as edges.

$n$ nodes: $0 \leq$ direct edges $\leq \frac{n(n-1)}{2}$

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
  def __repr__(self):
    return str(self.value)
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

## Walk (DFS)

```python
def walk_graph(p:Node):
    if p is None: return
    print(p.value)
    for q in p.edges:
        walk_graph(q)
```

### Avoiding cycle

```python
seen = set()
def walk_graph_no_cycle(p:Node):
    if p is None: return
    if p in seen: return
    seen.add(p)
    print(p.value)
    for q in p.edges:
        walk_graph_no_cycle(q)
        
walk(cat, set())
```

##Search

###Depth-first Search

Visits all reachable nodes from p, avoiding cycles, and go deep first.

```python
def DFS(p:Node, visited=set()):
    if p in vistited: return
    visited.add(p)
    for q in p.edges:
        DFS(q, visited)
```

For $n$ nodes, $m$ edges, $m$ can be $n^2$:

$O(n,m) = n+m$

### Breath-first Search

Visit all children then grandchildren.

```python
def BFS(root:Node):
    visited = {root}
    worklist = [root]
    while len(worklist)>0:
        p = worklist.pop(0)	# remove and return the index 0 value
        print(f"Visit {p}")
        for q in p.edges:
            if q not in visited:
                worklist.append(q)
                viisted.add(q)
```

`append` + `pop[0]` make the `wordlist` works as queue.

## Sort

### Topological Sort

postorder traversal via DFS

```python
def postorder(p:Node, sorted:set, visited:set):
    if p in visited: return
    visited.add(p)
    for q in p.edges:
        postorder(q, sorted, visited)
    sorted.append(p)
```

```python
def toposort(nodes):
    sorted = []
    visited = set()
    while len(visited) < len(nodes):
        todo = [node for node in nodes.values() if node not in visited]
        if len(todo)>0:
            postorder(todo[0], sorted, visited)
    return reverse(sorted)
```



## Common Questions

### Is `q` reachable from `p`?

####Find set of nodes $p$ can reach.

```python
def reachable(p:Node) -> set:
    reaches = set();
    DFS_reach(p, reaches, set())
    return reaches

def DFS_reach(p:Node, reaches:set, visited:set):
    if p in visited: return
    visited.add(p)
    for q in p.edges:
        reaches.add(q)
        DFS_reach(q, reaches, visited)
```

#### Find set of nodes $p$ can reach, track depth.

```python
def reachable(p:Node) -> dict:
    reaches = dict();
    DFS_reach_track(p, reaches, set(), depth=0)
    return reaches

def DFS_reach_track(p:Node, reaches:dict, visited:set, depth:int):
    if p in visited: return
    visited.add(p)
    reaches[p] = depth
    for q in p.edges:
        DFS_reach_track(q, reaches, visited, depth+1)
```

#### Find path from $p$ to $q$.

```python
def path(p:Node, q:Node) -> list:
    return DFS_path(p, q, [p], set())

def DFS_path(p:Node, q:Node, path:list, visited:set):
    if p is q: return path
    if p in visited return None
	visited.add(p)
    for t in p.edges:
        pa = DFS_path(t, q, path+[t], visited)
        if pa is not None: return pa
    return None
```

### Which nodes are within `k` edges of node `p` (neighborhood)?

```python
def neighbors(p:Node, k:int) -> dict:
    reaches = dict();
    DFS_neighbors(p, k, reaches, set(), depth=0)
    return reaches

def DFS_neighbors(p:Node, k:int, reaches:dict, visited:set, depth:int):
    if p in visited or depth>k: return
    visited.add(p)
    reaches[p] = depth
    for q in p.edges:
        DFS_neighbors(q, k, reaches, visited, depth+1)
```

### How many edges are on paths between `q` and `p`?

### Is graph connected (reach any `p` from any `q`)?

### Is graph cyclic (`p` reaches `p` traversing at least one edge)?

```python
def DFS_cyclic(start:Node, p:Node, visited) -> bool:
    if p in visited:
        if p is start: return True
        return False
    visited.add(p)
    for q in p.edges:
        c = DFS_cyclic(start, q, visited)
        if c: return True
       return False

def iscyclic(p:Node) -> bool:
    return DFS_cyclic(p,p,set())
```

### What is shortest path (num edges) from `p` to `q`?

```python
def BFS_shortest(root:Node, target:Node):
    visited = {root}
    worklist = [[root]]
    while len(worklist)>0:
        path = worklist.pop(0)
        p = path[-1]
        if p is target: return path
        for q in p.edges:
            if q not in visited:
                worklist.append(path+[q])
                visited.add(q)
```

