# DFS& BFS

## Breadth first search

### Methods

- Iteration with queue

### Questions Classify

- Traversal in Tree or Graph
  - [Binary Tree Level order traversal](tree.md/ "level-order")
  - [Graph level order traversal](graph.md/#bfs) TODO
  - [Matrix traversal](matrix.md/#traverse)
- [Connected component](graph.md/)
- [Topological Sorting](graph.md/#topo-sort)
- Shortest path

### Attention

- If handle inside the for loop, don't forget the first one outside the loop;
- 

## Depth first search (Backtracking)

### Methods

- Recursion

  ```python
  # handle empty case
  # (option) sort
  # recursion
  
  # recusrion defination
  	# recursion exit
    # recursion break into small component
    	# add new element
      # call recursion
      # remove added element
  ```

- Non-recursion

### Questions Classify

- Combination
- Permutation
- Finding all feasible solutions

### Attention

- end case and when to add to return set;
- shadow copy, or the parameter of recursion function:
  - use `deepcopy()` to create a deep copy;
  - use `nums[index+1:]+nums[:index]`

#### How to remove duplicate

> Avoid to find all solutions and then remove duplicate, this will waste lots of time.

1. Find a representative;
2. Create a rule for those representative, such as sort from smallest to largest;
3. Follow the rule to 

## Leetcode

## BFS

### [Binary Tree Level order traversal](../DS/tree.md)

### [Graph level order traversal](../DS/graph.md/#bfs) TODO

### Matrix Traverse

#### 200. Number of Islands

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        self.ans = 0
        if not grid: return self.ans
        for r in range(len(grid)):
            for c in range(len(grid[0])):
                if grid[r][c] == '1':
                    self.ans += 1
                    grid[r][c] = '0'
                    queue = [(r,c)]
                    # print(queue, self.ans)
                    while queue:
                        i,j = queue.pop(0)

                        if (i+1<len(grid)) and (grid[i+1][j]=='1'):
                            queue.append((i+1, j))
                            grid[i+1][j] = '0'
                        if (i-1>=0) and (grid[i-1][j]=='1'):
                            queue.append((i-1, j))
                            grid[i-1][j] = '0'
                        if (j+1<len(grid[0])) and (grid[i][j+1]=='1'):
                            queue.append((i, j+1))
                            grid[i][j+1]='0'
                        if (j-1>=0) and (grid[i][j-1]=='1'):
                            queue.append((i, j-1))
                            grid[i][j-1]='0'
        return self.ans
```

#### 286. Walls and Gates

```python
class Solution:
    def wallsAndGates(self, rooms: List[List[int]]) -> None:
        """
        Do not return anything, modify rooms in-place instead.
        """
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

#### 130. Surrounded Regions

```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        if not board: return
        rowN, colN = len(board), len(board[0])
        self.visited = set()
        for n in range(colN):
            if board[0][n] == 'O':
                queue = [(0,n)]
                self.visited.add((0,n))
                self.bfs(queue, rowN, colN, board, "check")
            if board[rowN-1][n] == 'O':
                queue = [(rowN-1,n)]
                self.visited.add((rowN-1,n))
                self.bfs(queue, rowN, colN, board, "check")
        for n in range(rowN):
            if board[n][0] == 'O':
                queue = [(n,0)]
                self.visited.add((n,0))
                self.bfs(queue, rowN, colN, board, "check")
            if board[n][colN-1] == 'O':
                queue = [(n,colN-1)]
                self.visited.add((n,colN-1))
                self.bfs(queue, rowN, colN, board, "check")
        # print(self.visited)
        
        for r in range(1, rowN-1):
            for c in range(1, colN-1):
                if board[r][c] == 'O' and (r,c) not in self.visited:
                    board[r][c]='X'
                    queue = [(r,c)]
                    self.bfs(queue, rowN, colN, board, "change")
                
            
    def bfs(self, queue, rowN, colN, board, method):
        direction = [(1,0), (-1,0), (0,1), (0,-1)]
        while queue:
            i, j = queue.pop(0)
            for dirX, dirY in direction:
                newi = i+dirX
                newj = j+dirY
                if newi>=0 and newi<rowN and newj>=0 and newj<colN and board[newi][newj]=='O' and (newi,newj) not in self.visited:
                    if method == 'check':
                        self.visited.add((newi,newj))
                    else:
                        board[newi][newj] = 'X'
                    queue.append((newi,newj))
```

### [Connected component](../DS/graph.md/)

### [Topological Sorting](../DS/graph.md/#topo-sort)

### Shortest path

#### 127. Word Ladder

```python
from collections import defaultdict
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        if endWord not in wordList: return 0
        
        wordDict = defaultdict(list)
        for word in wordList:
            for i in range(len(beginWord)):
                wordDict[word[:i]+'*'+word[i+1:]].append(word)

        queue = [(beginWord, 1)]
        visited = {beginWord: True}
        while queue:
            startWord, deep = queue.pop(0)
            for i in range(len(startWord)):
                temp_word = startWord[:i]+'*'+startWord[i+1:]
                for word in wordDict[temp_word]:
                    if word == endWord: 
                        return deep+1
                    if word not in visited:
                        visited[word] = True
                        queue.append((word, deep+1))
                wordDict[temp_word] = []
        return 0
```

## DFS & Backtracking

### Combinations

#### 39. Combination Sum

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort(reverse=True)
        ans = []
        for index, num in enumerate(candidates):
            if num>target: continue
            if target%num == 0: ans.append([num]*(target//num))
            if index+1<len(candidates):
                for n in range(target//num):
                    remind = target - num*(n+1)
                    temp = self.combinationSum(candidates[index+1:], remind)
                    if temp:
                        for row in temp:
                            row.extend([num]*(n+1))
                            ans.append(row)
        return ans
```

#### 78. Subsets

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        self.ans = []
        self.ans.append([])
        if not nums: return self.ans
        nums.sort()
        for idx,num in enumerate(nums):
            self.ans.append([num])
            self.dfs([num], nums[:idx]+nums[idx+1:])
            
        return self.ans

    def dfs(self, subset, nums):
        if not nums: return
        for idx, num in enumerate(nums):
            if num < subset[-1]: continue
            self.ans.append(subset+[num])
            self.dfs(subset+[num], nums[:idx]+nums[idx+1:])
```

#### 77. Combinations

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        if n<k: return []
        self.ans = []
        nums = list(range(1,n+1))
        for idx, num in enumerate(nums):
            subset = [num]
            if len(subset) == k: self.ans.append(subset)
            else: self.dfs(subset, nums[:idx]+nums[idx+1:], k)
        return self.ans
    
    def dfs(self, subset, nums, k):
        # print(subset)
        if not nums: return
        for idx, num in enumerate(nums):
            if num < subset[-1]: continue
            newset = subset+[num]
            if len(newset) == k: self.ans.append(newset)
            else: self.dfs(newset, nums[:idx]+nums[idx+1:], k)
```



### Permutations

#### 46. Permutations

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        self.ans = []
        n = len(nums)
        self.permuteCon(nums, [], n)
        return self.ans

    def permuteCon(self, nums: List[int], numList, n):
        print(numList, nums)
        if len(numList) == n:
            self.ans.append(numList)
            return
        for index, num in enumerate(nums):
            numList.append(num)
            self.permuteCon(nums[index+1:]+nums[:index], numList.copy(), n)
            numList.pop()
```

#### 22. Generate Parentheses

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        if n == 0: return ['']
        self.ans = []
        temp = ''
        queue = 0
        nleft = nright = n
        self.validParenthesis(nleft, nright, '(', temp, queue)
        self.validParenthesis(nleft, nright, ')', temp, queue)
        return self.ans

    def validParenthesis(self, nleft, nright, para, prefix, queue):
            if para == '(':
                nleft -= 1
                queue += 1
                prefix += para
            else:
                if queue == 0: return
                queue -= 1
                nright -= 1
                prefix += para
            if nleft == 0 and nright == 0: self.ans.append(prefix)
            if nleft > 0: self.validParenthesis(nleft, nright, '(', prefix, queue)
            if nright > 0: self.validParenthesis(nleft, nright, ')', prefix, queue) 
```

### All Feasible solution

#### 17. Letter Combinations of a Phone Number

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits: return []
        mapDict = {'2':'abc', '3':'def', '4':'ghi', '5':'jkl',
                   '6':'mno', '7':'pqrs', '8':'tuv', '9':'wxyz'}
        self.ans = []
        self.letterMap('', mapDict, digits)
        return self.ans

    def letterMap(self, letters, mapDict, digits):
        if not digits: 
            self.ans.append(letters)
            return
        if digits[0] not in mapDict: 
            return
        else:
            for letter in mapDict[digits[0]]:
                self.letterMap(letters+letter, mapDict, digits[1:])
```

#### 200. Number of Islands

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        self.ans = 0
        if not grid: return self.ans
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if not grid[i][j]: continue
                if grid[i][j] == '1':
                    self.findIslands(grid, i, j)
                    self.ans += 1
        return self.ans
        
    def findIslands(self, grid, i, j):
        if i<0 or j<0 or i>len(grid)-1 or j>len(grid[0])-1: return True
        if not grid[i][j]: return True
        if grid[i][j] == '0': return True
        grid[i][j] = False
        if self.findIslands(grid, i+1, j) and self.findIslands(grid, i-1, j) and self.findIslands(grid, i, j+1) and self.findIslands(grid, i, j-1): return True
```



#### 332. Reconstruct Itinerary

```python
class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        if not tickets: return ['JFK']
        itineraryDict = {}
        for [itFrom, itTo] in tickets:
            if itFrom not in itineraryDict:
                itineraryDict[itFrom] = [itTo]
            else:
                itineraryDict[itFrom].append(itTo)
        # print(itineraryDict)

        return self.connectItinerary(itineraryDict, ['JFK'], 'JFK', len(tickets))
    
    def connectItinerary(self, itinerarys, current, start, n):
        if start in itinerarys: 
            itinerarys[start].sort()
            for stop in itinerarys[start]:
                copy_dict = copy.deepcopy(itinerarys)
                copy_dict[start].remove(stop)
                itinerary = self.connectItinerary(copy_dict, current+[stop], stop, n)
                
                if len(itinerary) == (1+n):
                    return itinerary
        return current
```

#### 79. Word Search

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        if not word or not board: return False
        n = len(board)
        m = len(board[0])
        for i in range(n):
            for j in range(m):
                if self.find(board, i, j, n, m, word): return True
        return False
    
    def find(self, board, i, j, n, m, word):
        # print(i, j, word)
        if not word: return True
        if i < 0 or i > n-1 or j < 0 or j > m-1: return False
        if board[i][j] == word[0]:
            current = board[i][j]
            board[i][j] = '*'
            if self.find(board, i-1, j, n, m, word[1:]): return True
            if self.find(board, i+1, j, n, m, word[1:]): return True
            if self.find(board, i, j-1, n, m, word[1:]): return True
            if self.find(board, i, j+1, n, m, word[1:]): return True
            board[i][j] = current
        else:
            return False
```

