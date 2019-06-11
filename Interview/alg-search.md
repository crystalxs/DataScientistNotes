# Search

## Methods

### Binary Search

```python
def binsearch(nums, target):
    left = 0
    right = len(a)-1
    while left+1 < right:
        mid = (left+right)//2
        if nums[mid] == target:
            left = mid
        elif target < nums[mid]:
            right = mid + 1
        else:
            left = mid - 1
    if nums[right] == target: return right
    if nums[left] == target: return left
    return -1
```

## Questions Classify

- Search special number: binary search
- Search any/first/last position of numbers qualified special condition: binary search
- String Search

## Attention

- If can use non-recursion without recursion.
- Binary search end statement:
  - `start <= end`
  - `start < end` will lead to dead loop when finding last position.
  - `start + 1 < end`
- Check each condition (`==`, `>`, `<`) separate to make sure won't combine wrong conditions.

## Leetcode

### Position for special condition

#### 34. Find First and Last Position of Element in Sorted Array

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        ans = [-1, -1]
        if not nums: return ans
        left = 0
        right = len(nums)-1
        while left+1 < right:
            mid = (left+right)//2
            if nums[mid] == target:
                left = mid
            elif nums[mid] < target:
                left = mid+1
            else:
                right = mid-1
        if nums[right] == target: ans[1] = right
        elif nums[left] == target: ans[1] = left
        else: return ans
        
        left = 0
        right = ans[1]
        while left+1 < right:
            mid = (left+right)//2
            if nums[mid] == target:
                right = mid
            elif nums[mid] < target:
                left = mid+1
            else:
                right = mid-1
        if nums[left] == target: ans[0] = left
        elif nums[right] == target: ans[0] = right
        
        return ans
```

#### 278. First Bad Version

```python
# The isBadVersion API is already defined for you.
# @param version, an integer
# @return a bool
# def isBadVersion(version):

class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        left = 1
        right = n
        while left+1 < right:
            # print(left, right)
            mid = (left+right)//2
            if not isBadVersion(mid):
                left = mid+1
            else:
                right = mid
        if isBadVersion(left): return left
        else: return right
```

#### 153. Find Minimum in Rotated Sorted Array

> Find the **first** position of the number less than or equal to the last element in the array.

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        target = nums[-1]
        left = 0
        right = len(nums)-1
        while left+1 < right:
            mid = (left+right)//2
            if nums[mid] <= target:
                right = mid
            else:
                left = mid
        if nums[left]<=target: return nums[left]
        else: return nums[right]
```

####81. Search in Rotated Sorted Array II

```python
def search(self, nums: List[int], target: int) -> bool:
    self.ans=False
    n=len(nums)
    if n==0: return self.ans
    
    left=0
    right=n-1
    while left<=right:
        mid=(left+right)//2
        if nums[mid]==target:
            self.ans=True
            break
            
        if nums[left]==nums[mid]==nums[right]: # at one sub-list contain same value
            left+=1
            right-=1
        elif nums[left]<=nums[mid]: # left half is ascending
            if target>=nums[left] and target<=nums[mid]:
                right=mid-1
            else:
                left=mid+1
        else: # right half is ascending
            if target>=nums[mid] and target<=nums[right]:
                left=mid+1
            else:
                right=mid-1
    return self.ans
```
#### 33. Search in Rotated Sorted Array

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if not nums: return -1
        
        left = 0
        right = len(nums)-1
        while left <= right:
            mid = (right+left)//2
            
            # check equal conditions
            if nums[mid] == target: return mid
            if nums[left] == target: return left
            if nums[right] == target: return right
            
            if nums[left] < nums[mid]:
              	# left side is non-rotate, check if target in the non-rotate side
                if nums[left] < target and nums[mid] > target:
                    right = mid-1
                else:
                    left = mid+1
            else:
              	# right side is non-rotate, check if target in the non-rotate side
                if nums[mid] < target and nums[right] > target:
                    left = mid+1
                else:
                    right = mid-1
        return -1
```

#### 74. Search a 2D Matrix

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        if not matrix or not matrix[0]: return False
        first = (0,0)
        last = (len(matrix)-1, len(matrix[0])-1)
        while first[0] <= last[0]:
            if first[0] == last[0]:
                while first[1]+1 < last[1]:
                    mid = (first[0], (first[1]+last[1])//2)
                    if matrix[mid[0]][mid[1]] == target: return True
                    elif matrix[mid[0]][mid[1]] > target:
                        last = (mid[0], mid[1]-1)
                    else:
                        first = (mid[0], mid[1]+1)
                if matrix[first[0]][first[1]] == target: return True
                elif matrix[last[0]][last[1]] == target: return True
                else: return False
            mid = ((first[0]+last[0])//2, last[1])
            if matrix[mid[0]][mid[1]] == target: return True
            elif matrix[mid[0]][mid[1]] > target:
                last = mid
            else:
                first = (mid[0]+1, first[1])
```

#### 240. Search a 2D Matrix II

```python
class Solution:
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if not matrix or not matrix[0]: return False
        for nums in matrix:
            left = 0
            right = len(nums)-1
            while left <= right:
                mid = (left+right)//2
                if nums[mid] == target: return True
                elif nums[mid] > target:
                    right = mid-1
                else:
                    left = mid+1
        return False
```



### Delete Not Qualified Half

#### 852. Peak Index in a Mountain Array

```python
class Solution:
    def peakIndexInMountainArray(self, A: List[int]) -> int:
        left = 0
        right = len(A)-1
        while left+1 < right:
            mid = (right+left)//2
            if A[mid-1] > A[mid]:
                right = mid
            else:
                left = mid
        if A[left] > A[right]: return left
        else: return right
```

#### 162. Find Peak Element

```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        if not nums: return -1
        if len(nums) == 1: return 0
        left = 0
        right = len(nums)-1
        while left+1 < right:
            mid = (left+right)//2
            if nums[mid]>nums[mid-1] and nums[mid]>nums[mid+1]: return mid
            if nums[mid]<nums[mid+1]:
                left = mid+1
            else:
                right = mid-1
        if nums[left]>nums[right]: return left
        else: return right
```

### IDK

#### 4. Median of Two Sorted Arrays

```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        if len(nums1)==0:
            self.ans = (nums2[(len(nums2)//2)]+nums2[int((len(nums2)-1)/2)])/2
        elif len(nums2)==0:
            self.ans = (nums1[(len(nums1)/2)]+nums1[int((len(nums1)-1)/2)])/2
        else:
            totlen=len(nums1)+len(nums2)
            self.ans = (self.findTarget(nums1,nums2,(totlen+1)//2)+self.findTarget(nums1,nums2,(totlen+2)//2))/2
        return self.ans
    
    def findTarget(self, nums1, nums2, k)->int:
        # print(k,nums1,nums2, min(nums1[0], nums2[0]))
        if k==1: 
            if len(nums1)==0: return nums2[0]
            elif len(nums2)==0: return nums1[0]
            else: return min(nums1[0],nums2[0])
        if len(nums1)<k//2:
            return self.findTarget(nums1, nums2[k//2:], k-k//2)
        if len(nums2)<k//2:
            return self.findTarget(nums1[k//2:], nums2, k-k//2)
        else:
            if nums1[k//2-1]<nums2[k//2-1]:
                return self.findTarget(nums1[k//2:],nums2,k-k//2)
            else:
                return self.findTarget(nums1, nums2[k//2:],k-k//2)
```

