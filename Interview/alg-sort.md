# Sort

## Leetcode

#### 75. Sort Colors

```python
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        maxnum = max(nums)
        pigeon = [0]*(maxnum+1)
        for num in nums:
            pigeon[num] += 1
        head = 0
        for i, count in enumerate(pigeon):
            nums[head:head+count] = [i]*count
            head = head+count
```

#### 56.Merge Intervals

```python
# Definition for an interval.
# class Interval(object):
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution(object):
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        self.quicksort(intervals, 0, len(intervals)-1)
        i = 0
        try:
            while intervals[i+1]:
                if intervals[i].end >= intervals[i+1].start:
                    if intervals[i].end <= intervals[i+1].end:
                        intervals[i].end = intervals[i+1].end
                        intervals.pop(i+1)
                    else:
                        intervals.pop(i+1)
                else:
                    i += 1
        except: return intervals
        
    def quicksort(self, intervals, lo, hi):
        if lo >= hi: return
        pivot_idx = self.partition(intervals, lo, hi)
        self.quicksort(intervals, lo, pivot_idx-1)
        self.quicksort(intervals, pivot_idx+1, hi)
    
    def partition(self, intervals, lo, hi):
        i = lo
        pivot = intervals[hi].start
        for j in range(lo, hi):
            if intervals[j].start < pivot:
                intervals[j], intervals[i] = intervals[i], intervals[j]
                i += 1
        intervals[i], intervals[hi] = intervals[hi], intervals[i]
        return i
```

#### 148. Sort List

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def sortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next: return head
        dummy = ListNode(None)
        dummy.next = head
        
        pre = slow = fast = head
        while fast and fast.next:
            pre = slow
            slow = slow.next
            fast = fast.next.next
        pre.next = None
        left_list = self.sortList(head)
        right_list = self.sortList(slow)
        return self.merge(left_list, right_list)
    
    def merge(self, left_list, right_list):
        dummy = ListNode(None)
        p = dummy
        while left_list and right_list:
            if left_list.val>right_list.val:
                p.next, right_list= right_list, right_list.next
            else:
                p.next, left_list = left_list, left_list.next
            p = p.next
        if left_list:
            p.next = left_list
        else:
            p.next = right_list
        return dummy.next
```