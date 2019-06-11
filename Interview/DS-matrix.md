# Matrix

## Methods

1. convert
   - `directionX = [1,0,0,-1]` and `directionY = [0, 1, -1, 0]`
2. check inbound

## Attention

* `memo = [[False]*len(s) for _ in range(len(s))]` not equal to `memo = [[False]*lens(s)]*len(s)`, the second one will create a list of a list and its reference.

  ![image-20190608145056240](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/Interview/img/times.png)

## Questions Classify

### [Traversal](../algorithm/dfs&bfs.md/)

```python
class Solution:
    def wallsAndGates(self, rooms: List[List[int]]) -> None:
        """
        Do not return anything, modify rooms in-place instead.
        """
        # handle empty case
        if not rooms: return
        
        rowN, columnN = len(rooms), len(rooms[0])
        for r in range(rowN):
            for c in range(columnN):
                if rooms[r][c] == 0:
                    queue = [(r,c,0)]
                    self.bfs(queue, rowN, columnN, rooms)
                    
    def bfs(self, queue, rowN, columnN, rooms):
        direction = [(1,0), (-1,0), (0,1), (0,-1)]
        while queue:
            i,j,n = queue.pop(0)
            for dirX, dirY in direction:
                newi, newj = i+dirX, j+dirY
                if newi>=0 and newi<rowN and newj>=0 and newj<columnN and rooms[newi][newj] > n+1:
                    rooms[newi][newj] = n+1
                    queue.append((newi, newj, n+1))
```

## Attention

- Pay attention to the index inside loop and outside loop, same name will mess up;
- 