# Array

## Questions Classify

- sort
- duplicate (use hash table)

## Methods

- Multi-pointers from begin and end or even med, in `python` commonly use index to be the pointer.
- [Hash table](Interview/hash.md)

- 

## Attention

- Boundary Check
  - Out of index
  - Ending points
- Length Check
  - Length = 0
  - Length = 1 (usually boundary)
  - Length = 2 (will decrease time complexity when using recursive)
- **Python specific attention**
  - Start index 0
  - Modify the array will change index
    - Do not delete element in array!!! Find another way
  - Array index=-1 is not out of range
  - Pay attention to shadow copy
- Two arrays
  - Check the length equal or not, exist or not

## Leetcode

1. Two Sum:** visit array
2. **Median of two sorted arrays:** divide and conquer
   - on target rather than array
3. **Container with most water:** two pointers
4. **Remove duplicates from sorted array:** two pointers
   - don't `pop` or `delete` element
   - exchange the position of unique element to front
5. **Jump Game:** bottom-up dynamic programming
   - use another array to record status
   - recursive will cost toooooo much
6. **Search in rotated sorted array:** binary search
7. **Rotate Array:** 
   - ideas: reverse twice / cyclic replacement / extra array
8. **Game of Life:** general visit matrix
   - make a copy to avoid change influence future

## 13. Roman to Integer

```python
class Solution(object):
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        num_map = {"I": 1,
                   "V": 5,
                   "X": 10,
                   "L": 50,
                   "C": 100,
                   "D": 500,
                   "M": 1000}
        reint = 0
        for i, num in enumerate(s):
            if i+1 < len(s):
                if num == 'I' and (s[i+1] == 'V' or s[i+1] == 'X'):
                    reint -= 1
                elif num == 'X' and (s[i+1] == 'L' or s[i+1] == 'C'):
                    reint -= 10
                elif num == 'C' and (s[i+1] == 'D' or s[i+1] == 'M'):
                    reint -= 100
                else:
                    reint += num_map[num]
            else:
                reint += num_map[num]
        return reint
        
```

## 1. Two Sum

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i, ele in enumerate(nums):
            new_target = target - ele
            for j, num in enumerate(nums):
                if i != j and num==new_target:
                    return [i,j]
```

## 53. Maximum Subarray

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        for index in range(1,len(nums)):
            if nums[index-1] > 0:
                nums[index] += nums[index-1]
        return max(nums)
```

## 15. 3Sum

### Idea

- Sort at the beginning;
- Avoid use `in` to check duplicate;

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        sol = []
        nums.sort()
        i = 0
        while i<len(nums):
            target = 0-nums[i]
            right = len(nums)-1
            left = i+1
            while left < right:
                if nums[right]+nums[left]==target:
                    ans = [nums[i], nums[left], nums[right]]
                    sol.append(ans)
                    while left+1 < right and nums[left+1] == nums[left]:
                        left = left + 1
                    while right-1 > left and nums[right-1] == nums[right]:
                        right = right - 1
                    left += 1
                    right -= 1
                elif nums[right]+nums[left]>target:
                    right -= 1
                else:
                    left += 1
            while i+1 < len(nums) and nums[i+1] == nums[i]: i+=1
            i+=1
        return sol
```

## 18. 4Sum

**Idea**: same as [15. 3Sum](#15. 3Sum)

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        sol = []
        nums.sort()
        i = 0
        while i<len(nums):
            target1 = target-nums[i]
            j = i+1
            while j<len(nums):
                target2 = target1-nums[j]
                right = len(nums)-1
                left = j+1
                while left < right:
                    if nums[right]+nums[left]==target2:
                        ans = [nums[i], nums[j], nums[left], nums[right]]
                        sol.append(ans)
                        while left+1 < right and nums[left+1] == nums[left]:
                            left = left + 1
                        while right-1 > left and nums[right-1] == nums[right]:
                            right = right - 1
                        left += 1
                        right -= 1
                    elif nums[right]+nums[left]>target2:
                        right -= 1
                    else:
                        left += 1
                while j+1 < len(nums) and nums[j+1] == nums[j]: j+=1
                j+=1
            while i+1 < len(nums) and nums[i+1] == nums[i]: i+=1
            i+=1
        return sol
```

## 54. Spiral Matrix

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        ans=[]
        while matrix:
            ans.extend(matrix[0])
            matrix = matrix[1:]
            if not matrix: return ans
            for row in matrix:
                ans.append(row.pop())
            matrix = [row for row in matrix if row]
            if not matrix: return ans
            ans.extend(matrix.pop()[::-1])            
            if not matrix: return ans
            for row in matrix[::-1]:
                ans.append(row.pop(0))
            matrix = [row for row in matrix if row]
        return ans
```

## 121. Best Time to Buy and Sell Stock

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices: return 0
        ans = 0
        lowest = prices[0]
        for price in prices[1:]:
            if price < lowest:
                lowest = price
            elif price - lowest > ans:
                ans = price - lowest
        return ans
```

## 39. Combination Sum

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

