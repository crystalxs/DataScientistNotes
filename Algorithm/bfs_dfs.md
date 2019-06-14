# BFS & DFS

## Breadth first search

### When to used

* Traversal in Tree or Graph
  * [Binary Tree Level order traversal](../DS/tree.md/#bfs)
  * [Graph level order traversal]()
  * Connected component
  * Topological Sorting
* Shortest path

### Implement

#### Queue

```python
# 1. create queue
queue = []
# 2. while queue is not empty
while queue:
  # 3. from x to x+1 level
```



#### Recursive

### Level order traversal on Tree



## Depth first search (Backtracking)

> <https://www.geeksforgeeks.org/backtracking-algorithms/>
>
> <https://www.geeksforgeeks.org/backtracking-introduction/>
>
> Used for finding all feasible solutions and save space complexity.

Incrementally builds candidate to the solution and abandons a candidate (“backtracks”) as soon as it determines that the candidate cannot possibly be completed to a valid solution, can be solved by Backtracking.

1. The Algorithm begins to build up a solution, starting with an empty solution set S.
2. Add to S the first move that is still left (all possible moves are added to S one by one). This now creates a new sub-tree s in the search tree of the algorithm.
3. Check if S+s satisfies each of the constraints:
   - If Yes, then the sub-tree s is “eligible” to add more “children”.
   - Else, the entire sub-tree s is useless, so recurs back to step 2 using argument S.
4. In the event of “eligibility” of the newly formed sub-tree s, recurs back to step 2, using argument S+s.
5. If the check for S+s returns that it is a solution for the entire data. Output and terminate the program.
   If not, then return that no solution is possible with the current s and hence discard it.

### Decision Problem

> we search for a feasible solution.

### Optimization Problem

> we search for the best solution.

### Enumeration Problem

> we find all feasible solutions.

