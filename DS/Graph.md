# Graph

> * A collection of connected element pairs
> * The aggregate of nodes

## Definition

> <http://interactivepython.org/courselib/static/pythonds/Graphs/VocabularyandDefinitions.html>

**Nodes / vertices** connected with **edges**, which can have **labels**.

Directed graph have arrows as edges; undirected graph use lines as edges.

For $n$ nodes: $0 \leq$ direct edges $\leq \frac{n(n-1)}{2}$

## Operations

- `Graph()` creates a new, empty graph.
- `addVertex(vert)` adds an instance of `Vertex` to the graph.
- `addEdge(fromVert, toVert)` Adds a new, directed edge to the graph that connects two vertices.
- `addEdge(fromVert, toVert, weight)` Adds a new, weighted, directed edge to the graph that connects two vertices.
- `getVertex(vertKey)` finds the vertex in the graph named `vertKey`.
- `getVertices()` returns the list of all vertices in the graph.
- `in` returns `True` for a statement of the form `vertex in graph`, if the given vertex is in the graph, `False` otherwise.

##Implementation

###Adjacency matrix implementations

> $n \times n$ matrix, each of the rows and columns represent a vertex in the graph; {0,1} if unlabeled or {labels} if edges are labeled; undirected matrices are symmetric.

- Simple;
- Wastes space for sparse edges -> using sparse matrix.
- Fast to access arbitrary node's edges.

###Adjacency list implementations

> Keep a master list of all the vertices in the Graph object and then each vertex object in the graph maintains a list of the other vertices that it is connected to.

- Fast arbitrary node access for numbered nodes;
- Space efficient.

#### Implementation in Python

`Graph`: holds the master list of vertices;

`Vertex`: represent each vertex in the graph.

```python
class Vertex:
    def __init__(self,key):
        self.id = key
        self.connectedTo = {}

    def addNeighbor(self,nbr,weight=0):
        self.connectedTo[nbr] = weight

    def __str__(self):
        return str(self.id) + ' connectedTo: ' + str([x.id for x in self.connectedTo])

    def getConnections(self):
        return self.connectedTo.keys()

    def getId(self):
        return self.id

    def getWeight(self,nbr):
        return self.connectedTo[nbr]


class Graph:
    def __init__(self):
        self.vertList = {}
        self.numVertices = 0

    def addVertex(self,key):
        self.numVertices = self.numVertices + 1
        newVertex = Vertex(key)
        self.vertList[key] = newVertex
        return newVertex

    def getVertex(self,n):
        if n in self.vertList:
            return self.vertList[n]
        else:
            return None

    def __contains__(self,n):
        return n in self.vertList

    def addEdge(self,f,t,cost=0):
        if f not in self.vertList:
            nv = self.addVertex(f)
        if t not in self.vertList:
            nv = self.addVertex(t)
        self.vertList[f].addNeighbor(self.vertList[t], cost)

    def getVertices(self):
        return self.vertList.keys()

    def __iter__(self):
        return iter(self.vertList.values())
```

###Connected nodes implementation

- Most common implementation due to nice mapping to objects.
- Each node has info about node and edge list.

#### Implementation in Python

```python
class Node:
  def __init__(self, value):
    self.value = value
    self.edges = [] # outgoing edges
    # Use list or dictionary index if you need to access nodes directly.
  def add(self, target:Node):
    self.edges.append(target)
  def __repr__(self):
    return str(self.value)
```

##### With labels

```python
class LNode:
    def __init__(self, value):
        self.value = value
        self.edges = {}
		def add(self, label, target):
        self.edges[label] = target
```

## Walk

###Depth-first Search

> Visits all reachable nodes from p, avoiding cycles, and go deep first.

```python
def DFS(p:Node, visited=set()):
    if p in vistited: return
    visited.add(p)
    for q in p.edges:		# use for to track the worklist
        DFS(q, visited)
```

####Performance

For $n$ nodes, $m$ edges: $O(n,m) = n+m$ ($m$ can be $n^2$).

### Breath-first Search

> Proceeds by exploring edges in the graph to find all the vertices in G for which there is a path from s;
>
> Visit all children then grandchildren.

To keep track of its progress, BFS colors each of the vertices white, gray, or black:

* All the vertices are initialized to white when they are constructed.
* When a vertex is initially discovered it is colored gray;
* When BFS has completely explored a vertex it is colored black;
* A white vertex is an undiscovered vertex;
* This means that once a vertex is colored black, it has no white vertices adjacent to it;
* A gray node, on the other hand, may have some white vertices adjacent to it, indicating that there are still additional vertices to explore.

Use `append` + `pop[0]` make the `wordlist` works as queue:

```python
def BFS(root:Node):
    visited = {root}				# black
    worklist = [root]				# gray
    while len(worklist)>0:
        p = worklist.pop(0)	# remove and return the index 0 value
        print(f"Visit {p}")
        for q in p.edges:
            if q not in visited:
                worklist.append(q)
                visited.add(q)
```

#### Performance

##Topological Sort

> To help us decide the precise order in which we should do each of the steps required to make our pancakes we turn to a graph algorithm called the **topological sort**.
>
> A topological sort takes a directed acyclic graph and produces a linear ordering of all its vertices such that if the graph G contains an edge (v,w) then the vertex vv comes before the vertex w in the ordering. 

Post-order traversal via DFS:

* `sorted`: black vertices
* `visited`: gray vertices
* `todo`: white vertices

```python
def postorder(p:Node, sorted:set, visited:set):
    if p in visited: return
    visited.add(p)
    for q in p.edges:
        postorder(q, sorted, visited)
    sorted.append(p)


def toposort(nodes):
    sorted = []
    visited = set()
    while len(visited) < len(nodes):
        todo = [node for node in nodes.values() if node not in visited]
        if len(todo)>0:
            postorder(todo[0], sorted, visited)
    return reverse(sorted)
```

### Dijkstra's Algorithm

> Determine the shortest path.

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

#### Performance

### Prim’s Spanning Tree Algorithm

> <http://interactivepython.org/courselib/static/pythonds/Graphs/PrimsSpanningTreeAlgorithm.html>

### Strongly Connect Component

> We formally define a **strongly connected component**, C, of a graph G, as the largest subset of vertices C⊂V such that for every pair of vertices v,w∈C we have a path from v to w and a path from w to v.

1. Call `dfs` for the graph G to compute the finish times for each vertex.
2. Compute $G^T$.
3. Call `dfs` for the graph $G^T$ but in the main loop of DFS explore each vertex in decreasing order of finish time.
4. Each tree in the forest computed in step 3 is a strongly connected component. Output the vertex ids for each vertex in each tree in the forest to identify the component.