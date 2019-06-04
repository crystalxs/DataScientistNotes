# Graph

## Questions Classify

### DFS (non-recursive)

- use stack
- push targets in reverse order onto stack
- pop last stack item for node to process

### BFS

(non-recursive)

- use queue
- push targets in order onto queue
- pull from first position

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

### Topological Sorting <a name="topo-sort"/>

> Use BFS, and avoid using dfs.

```python
# 1. create hash to store the indegree for each node
# 2. find the nodes, which indegree are 0
# 3. bfs
```

#### Check whether or not can be done with topological sorting

> If there is no nodes in the left nodes with indegree is 0, then it cannot.

### Connection

```python
# 1. bfs
# 2. check if the visited node number equal to all nodes

def connection(root:Node,n):
  	if n == 0: return False
    visited = {root}				# black
    worklist = [root]				# gray
    while len(worklist)>0:
        p = worklist.pop(0)	# remove and return the index 0 value
        print(f"Visit {p}")
        for q in p.edges:
            if q not in visited:
                worklist.append(q)
                visited.add(q)
    return len(visited)==n
```



#### Is graph cyclic (`p` reaches `p` traversing at least one edge)?

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

#### Find set of nodes $p$ can reach.

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

##### How many edges are on paths between `q` and `p` (track depth)?

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

##### Which nodes are within `k` edges of node `p` (neighborhood)?

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

#### Find path from $p$ to $q$.

Tacking path not set of nodes.

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

### BFS

#### What is shortest path (num edges) from `p` to `q`?

```python
def shortest(root:Node, target:Node):
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

#### What is shortest path using edge weights?

#### Traveling salesman problem

## Leetcode

## BFS

### 133. Clone Graph

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, neighbors):
        self.val = val
        self.neighbors = neighbors
"""
class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        visited = {}
        dummy = Node(-1, [])
        queue = [(node, dummy)]
        while queue:
            current, parentNode = queue.pop(0)
            if current not in visited:
                currentNode = Node(current.val, [])
                parentNode.neighbors.append(currentNode)
                for neighbor in current.neighbors:
                    queue.append((neighbor,currentNode))
                visited[current] = currentNode
            else:
                parentNode.neighbors.append(visited[current])
        return dummy.neighbors[0]
```

## Topo Sort

#### 207. Course Schedule

```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        if numCourses < 2: return True 
        courses = {}
        for num in range(numCourses):
            courses[num] = []
        for target, request in prerequisites:
            courses[target].append(request)
        
        for course in range(numCourses):
            if len(courses[course])==0: continue # no prerequisites
            stack = courses[course]
            token = set(range(course))
            while stack:
                taking = stack.pop()
                if taking == course: return False
                if taking not in token:
                    token.add(taking)
                    if len(courses[taking])==0: continue # no prerequisites
                    else: 
                        for to_take in courses[taking]:
                            if to_take not in token: stack.append(to_take)
        return True
```

#### 210. Course Schedule II

```python
class Solution(object):
    def __init__(self):
        self.ans = []
        self.un_take = []
        self.waitlist = []
        
    def findOrder(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: List[int]
        """
        if numCourses == 1: return [0]
        
        courses = {}
        for course in range(numCourses):
            courses[course]=[]
        for target, request in prerequisites:
            courses[target].append(request)
        
        self.un_take = list(range(numCourses))
        while self.un_take:
            course = self.un_take.pop()
            self.takeCourse(course, courses)

        if -1 in self.ans: return []
        return self.ans
    
    def takeCourse(self, course, prerequisites):
        # check cycle
        if course in self.waitlist: 
            self.ans.append(-1)
            return
        
        # already take
        if course in self.ans: return
        
        # no prerequisites
        if len(prerequisites[course])==0: 
            self.ans.append(course)
            return
        
        # have prerequisites
        self.waitlist.append(course)
        for to_take in prerequisites[course]:
            self.takeCourse(to_take, prerequisites)
        if -1 not in self.ans:
            self.waitlist.remove(course)
            self.ans.append(course)
        return
```

