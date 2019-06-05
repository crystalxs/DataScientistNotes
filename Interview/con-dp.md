# Dynamic Programming

## Implementation

1. State
2. Function
3. **Initialization:** the smallest state;
4. **Answer: ** the biggest state.

### Classification

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

- Max or Min
- If feasible
- Count the feasible solutions number

### Questions cannot use DP

- Find all feasible solutions rather than counting the number, since dynamic programming can only find one of the best solution rather than all best solutions.
- Input is set rather than list (dynamic programming usually cannot change position);
- Time complexity for brute force is already polynomial level, dynamic programming can drop exponential time complexity to polynomial.

## Leetcode

### Min & Max (Bottom-Up)

#### 322. Coin Change

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

#### 198. House Robber

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

#### 70. Climbing Stairs

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n < 0: return 1

        way_list = [1]*(n+1)
        for idx in range(2, n+1):
            way_list[idx] = way_list[idx-1]+way_list[idx-2]
        return way_list[-1]
```

#### 256. Paint House

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

#### 746. Min Cost Climbing Stairs

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





