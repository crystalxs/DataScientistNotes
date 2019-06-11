# Dynamic Programming

## Implementation

1. State
2. Function
3. **Initialization:** the smallest state;
4. **Answer: ** the biggest state.

Every Dynamic Programming problem has a schema to be followed:

- Show that the problem can be broken down into optimal sub-problems.
- Recursively define the value of the solution by expressing it in terms of optimal solutions for smaller sub-problems.
- Compute the value of the optimal solution in bottom-up fashion.
- Construct an optimal solution from the computed information.

### Classification

> **Bottom up vs. Top Down:**
>
> In Top Down, you start building the big solution right away by explaining how you build it from smaller solutions.
>
> In Bottom Up, you start with the small solutions and then build up.

#### Coordinate

> 循环依赖，限制行动方向

**State** 

`f[x]`: from start point to x coordinate;

`f[x][y]`: from start point to (x,y) coordinate.

**Function:** how to go to (x,y) from last step.

**Initialize:** start point.

**Answer:** end point.

- 接龙
- 划分
- 匹配
- 背包
- 区间
- 数图
- 博弈

## Questions Classify

#### Optimization problems

> Select a feasible solution, so that the value of the required function is minimized or maximized. 

#### Combinatorial problems

> Figure out the number of ways to do something, or the probability of some event happening.

### Questions cannot use DP

- Find all feasible solutions rather than counting the number, since dynamic programming can only find one of the best solution rather than all best solutions.
- Input is set rather than list (dynamic programming usually cannot change position);
- Time complexity for brute force is already polynomial level, dynamic programming can drop exponential time complexity to polynomial.

## Leetcode

### Min & Max (Bottom-Up)

#### One Dimension

##### 322. Coin Change

1. Create a list to store the current min coins for each amount;
2. Update from smallest amount to largest amount;
3. Check if there is a feasible solution;
4. Return.

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        if amount < 1:
            return 0
        
        dp = [amount + 1] * (amount + 1)
        dp[0] = 0
        
        for amt in range(1, amount + 1):
            for coin in coins:
                if amt - coin >= 0:
                    dp[amt] = min(dp[amt], 1 + dp[amt - coin])
                    
        if dp[amount] > amount:
            return -1
        
        return dp[amount]
```

##### 70. Climbing Stairs

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n < 0: return 1

        way_list = [1]*(n+1)
        for idx in range(2, n+1):
            way_list[idx] = way_list[idx-1]+way_list[idx-2]
        return way_list[-1]
```

##### 746. Min Cost Climbing Stairs

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        # if not cost: return 0
        # if len(cost) == 1: return cost[0]
        if len(cost) <= 2: return 0
        n = len(cost)
        min_cost = [0]*(n+1)
        for i in range(2,n+1):
            min_cost[i] = min(min_cost[i-1]+cost[i-1],
                              min_cost[i-2]+cost[i-2])
        return min_cost[-1]
```

##### 300. Longest Increasing Subsequence

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if not nums: return 0

        length = [1]*len(nums)
        for idx in range(1, len(nums)):
            for point in range(idx):
                if nums[idx] > nums[point] and length[point]+1>length[idx]:
                    length[idx] = length[point]+1
        return max(length)
```

##### 354. Russian Doll Envelopes (LTE)

```python
class Solution:
    def maxEnvelopes(self, envelopes: List[List[int]]) -> int:
        if not envelopes: return 0
        sorted_envelopes = sorted(envelopes, key=lambda x: (x[0],x[1]))
        # print(sorted_envelopes)
        nums = [1]*len(sorted_envelopes)
        ans = 1
        for idx in range(1, len(sorted_envelopes)):
            for point in range(idx):
                if sorted_envelopes[idx][0]>sorted_envelopes[point][0] and sorted_envelopes[idx][1]>sorted_envelopes[point][1] and nums[point]+1>nums[idx]:
                    nums[idx] = nums[point]+1
            ans = max(ans, nums[idx])
        # print(nums)
        return ans
```

##### 368. Largest Divisible Subset

```python
class Solution:
    def largestDivisibleSubset(self, nums: List[int]) -> List[int]:
        if not nums: return []
        nums.sort()
        subset = [[1, [nums[idx]]] for idx in range(len(nums))]
        ans = [nums[0]]
        for idx in range(1, len(nums)):
            for j in range(idx):
                if (nums[idx]%nums[j] == 0 or nums[j]%nums[idx] == 0) and subset[j][0]+1>subset[idx][0]:
                    subset[idx][0] = subset[j][0]+1
                    subset[idx][1] = subset[j][1]+[nums[idx]]
            if subset[idx][0] > len(ans):
                ans = subset[idx][1]
        return ans
```

##### 403. Frog Jump

```python
class Solution:
    def canCross(self, stones: List[int]) -> bool:
        river = {stone: [] for stone in stones}
        river[0].append(0)
        for stone in stones:
            for step in river[stone]:
                for jump in (step-1, step, step+1):
                    if jump+stone == stones[-1]:
                        return True
                    elif jump+stone in river:
                        if not river[stone+jump] or river[stone+jump][-1]>jump:
                            river[stone+jump].append(jump)
        return False
```

##### 279. Perfect Squares (LTE)

```python
class Solution:
    def numSquares(self, n: int) -> int:
        if n < 1: return 0
        nums = [0]*(n+1)
        nums[1] = 1
        for num in range(2, n+1):
            # print(num, nums)
            if num**2 <= n: nums[num**2] = 1
            if nums[num] != 1:
                for i in range(1, num//2+1):
                    if nums[i]+nums[num-i]<nums[num] or not nums[num]:
                        nums[num]=nums[i]+nums[num-i]
        return nums[-1]
```



#### Two Dimension

##### 256. Paint House

```python
class Solution:
    def minCost(self, costs: List[List[int]]) -> int:
        if not costs: return 0
        n = len(costs)
        for i in range(1,n):
            temp = [costs[i][0], costs[i][1], costs[i][2]]
            costs[i][0] = min(temp[0]+costs[i-1][1], temp[0]+costs[i-1][2])
            costs[i][1] = min(temp[1]+costs[i-1][0], temp[1]+costs[i-1][2])
            costs[i][2] = min(temp[2]+costs[i-1][0], temp[2]+costs[i-1][1])
            # print(costs[i][0], costs[i][1], costs[i][2])
        return min(costs[-1])
```

##### 265. Paint House II

```python
class Solution:
    def minCostII(self, costs: List[List[int]]) -> int:
        if not costs or not costs[0]: return 0
        
        n = len(costs)
        k = len(costs[0])
        if n > 1 and k == 1: return 0
        mini_costs = [[0]*k for idx in range(n)]
        mini_costs[0] = costs[0]
        for i in range(1, n):
            for j in range(k):
                mini_costs[i][j] = costs[i][j] + min(mini_costs[i-1][:j]+mini_costs[i-1][j+1:])
        return min(mini_costs[-1])
```

##### 120. Triangle

```python
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        if not triangle: return 0
        path = [[0]*(idx+1) for idx in range(len(triangle))]
        path[0][0] = triangle[0][0]
        visited = set()
        
        for idx, level in enumerate(path[:-1]):
            for col, current in enumerate(level):
                if (idx+1, col) not in visited or current+triangle[idx+1][col] < path[idx+1][col]:
                    path[idx+1][col] = current+triangle[idx+1][col]
                    visited.add((idx+1, col))
                if (idx+1, col+1) not in visited or current+triangle[idx+1][col+1] < path[idx+1][col+1]:
                    path[idx+1][col+1] = current+triangle[idx+1][col+1]
                    visited.add((idx+1, col+1))

        return min(path[-1])
```

##### 64. Minimum Path Sum

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        if not grid: return 0
        m = len(grid)
        n = len(grid[0])
        path = [[0]*n for idx in range(m)]
        path[0][0] = grid[0][0]
        for row in range(m):
            for col in range(n):
                if row == 0 and col == 0: continue
                elif row == 0:
                    path[row][col] = path[row][col-1]+grid[row][col]
                elif col == 0:
                    path[row][col] = path[row-1][col]+grid[row][col]
                else:
                    path[row][col] = min(path[row-1][col], path[row][col-1])+grid[row][col]
        return path[-1][-1]
```

##### 72. Edit Distance

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        n1 = len(word1)
        n2 = len(word2)
        changes = [[0]*(n1+1) for i in range(n2+1)]

        # initial
        changes[0] = [i for i in range(n1+1)]
        for i in range(1, n2+1):
            changes[i][0] = i
        # print(changes)
        
        # dp
        for i in range(1, n2+1):
            for j in range(1, n1+1):
                if word1[j-1] == word2[i-1]:
                    changes[i][j] = 1+min(changes[i-1][j-1]-1, changes[i-1][j], changes[i][j-1])
                else:
                    changes[i][j] = 1+min(changes[i-1][j-1], changes[i-1][j], changes[i][j-1])
        # print(changes)
        return changes[-1][-1]
```

##### 97. Interleaving String

```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if not s1 and not s2 and not s3: return True
        if len(s1)+len(s2) != len(s3): return False
        n1 = len(s1)+1
        n2 = len(s2)+1
        matrix = [[False for j in range(n2)] for i in range(n1)]
        
        # initial
        for i in range(n2):
            if s2[:i] == s3[:i]:
                matrix[0][i] = s2[:i]
            if i == len(s3) and matrix[0][i]: return True
        for i in range(n1):
            if s1[:i] == s3[:i]:
                matrix[i][0] = s1[:i]
            if i == len(s3) and matrix[i][0]: return True
        
        # dp
        for i in range(1,n1):
            for j in range(1,n2):
                if matrix[i-1][j] and matrix[i-1][j]+s1[i-1] == s3[:i+j]:
                    matrix[i][j]=matrix[i-1][j]+s1[i-1]
                if matrix[i][j-1] and matrix[i][j-1]+s2[j-1] == s3[:i+j]:
                    matrix[i][j]=matrix[i][j-1]+s2[j-1]
                if i+j == len(s3) and matrix[i][j]: return True
        return False
```



#### Simplify

##### 198. House Robber

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums: return 0
        if len(nums) == 1: return nums[0]

        max_list = [0]*(len(nums))
        max_list[0] = nums[0]
        max_list[1] = max(nums[0], nums[1])
        for idx in range(2, len(nums)):
            max_list[idx] = max(max_list[idx-1], max_list[idx-2]+nums[idx])
        return max_list[-1]
```

### Count the feasible solutions number

#### 276. Paint Fence

Use math logic to calculate ways.

```python
class Solution:
    def numWays(self, n: int, k: int) -> int:
        if n < 1: return 0
        if n == 1: return k
        if k == 0: return 0
        if k == 1 and n > 2: return 0

        paint_ways = [k, k**2]
        adjacent = k
        for i in range(2, n):
            paint_ways.append(adjacent*(k-1)+(paint_ways[i-1]-adjacent)*k)
            adjacent=paint_ways[i-1]-adjacent
        # print(paint_ways)
                
        return paint_ways[-1]
```

#### 91. Decode Ways

```python
class Solution:
    def numDecodings(self, s: str) -> int:
        if not s: return 0
        if s[0] == '0': return 0
        
        n = len(s)
        ways = [0]*(n+1)
        ways[0] = 1
        ways[1] = 1
        for i in range (1, n):
            if s[i] != '0': ways[i+1] = ways[i]
            if int(s[i-1:i+1])<=26 and s[i-1]!='0':
                ways[i+1] += ways[i-1]
        return ways[-1]
```

#### 62. Unique Paths

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        path = [[0]*m for idx in range(n)]
        path[0][0] = 1
        for col in range(m):
            for row in range(n):
                if col == 0 and row == 0: continue
                elif col == 0:
                    path[row][col] = path[row-1][col]
                elif row == 0:
                    path[row][col] = path[row][col-1]
                else:
                    path[row][col] = path[row][col-1]+path[row-1][col]
        # print(path)
        return path[-1][-1]
```

#### 63. Unique Paths II

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if not obstacleGrid or not obstacleGrid[0]: return 1
        
        path = [[0]*len(obstacleGrid[0]) for idx in range(len(obstacleGrid))]
        for i in range(len(obstacleGrid)):
            for j in range(len(obstacleGrid[0])):
                if obstacleGrid[i][j] == 1: continue
                if i==0 and j==0:
                    path[i][j]=1
                    continue
                if i != 0: path[i][j] += path[i-1][j]
                if j != 0: path[i][j] += path[i][j-1]
        return path[-1][-1]
```



### String

> Not recommend using dp, sliding window is more easier to understand.

#### 139. Word Break

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        memo = [False]*(len(s)+1)
        memo[0] = True
        wordSet = set(wordDict)
        for idx in range(1,len(s)+1):
            for i in range(idx):
                if memo[i] and s[i:idx] in wordSet:
                    memo[idx] = True
                    break
        print(memo)
        return memo[-1]
```

#### 5. Longest Palindromic Substring

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        memo = [[False]*len(s) for _ in range(len(s))]
        start = 0
        end = 0

        for i in range(len(s)):
            left = i
            while left >= 0:
                if left == i:
                    # print("==", left, i)
                    memo[left][i] = True
                elif left+1 == i:
                    # print("+=", left, i)
                    memo[left][i] = s[left] == s[i]
                else:
                    # print("++", left, i)
                    memo[left][i] = (s[left] == s[i]) and memo[left+1][i-1]

                if memo[left][i] and (i-left+1) > (end-start+1):
                    start = left
                    end = i
                left = left-1
            # print(i,left, memo, start, end)
        return s[start:end+1]
```



