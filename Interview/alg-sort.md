# Sort

## Methods

### DSU

1. Decorate: a sequence by building a list of tuples with one or more sort keys preceding the elements from the sequence;
2. Sort: the list of tuples using the Python built-in `sort`;
3. Undecorate: by extracting the sorted elements of the sequence.

### Heap

1. Insert K elements into the min-heap or max-heap based on the problem.
2. Iterate through the remaining numbers and if you find one that is larger than what you have in the heap, then remove that number and insert the larger one.

There is no need for a sorting algorithm because the heap will keep track of the elements for you.

![img](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/Interview/img/heap.png)

## Questions Classify

- Quick Sort
- Top/smallest/frequent K elements: heap

## Attention

## Leetcode

### Quick Sort

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

#### 692. Top K Frequent Words

```python
class Solution:
    def topKFrequent(self, words: List[str], k: int) -> List[str]:
        words_dict = {}
        for word in words:
            if word not in words_dict:
                words_dict[word] = 1
            else:
                words_dict[word] += 1

        words_freq = list(words_dict.items())
        self.quicksort(words_freq, 0, len(words_freq)-1)
        return [word[0] for word in words_freq[-1:-k-1:-1]]
    
    def quicksort(self, sort_list, low, high):
        if low>=high: return
        pivot_idx = self.partition(sort_list, low, high)
        self.quicksort(sort_list, pivot_idx+1, high)
        self.quicksort(sort_list, low, pivot_idx-1)
        
    def partition(self, sort_list, low, high):
        pivot = sort_list[high][1]
        pivot_s = sort_list[high][0]
        i = low
        for j in range(low, high):
            if sort_list[j][1]<pivot or (sort_list[j][1] == pivot and sort_list[j][0] > pivot_s):
                sort_list[j], sort_list[i] = sort_list[i], sort_list[j]
                i += 1
        sort_list[high], sort_list[i] = sort_list[i], sort_list[high]
        return i
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

### Heap Sort

#### 215. Kth Largest Element in an Array

```python
# quick sort
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return heapq.nlargest(k, nums)[-1]

# quick sort
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        self.quicksort(nums, 0, len(nums)-1, len(nums)-k)
        return nums[-k]
    
    def quicksort(self, nums, low, high, k_small):
        if low >= high: return
        pivot_idx = self.partition(nums, low, high)
        if pivot_idx < k_small:
            self.quicksort(nums, pivot_idx+1, high, k_small)
        elif pivot_idx > k_small:
            self.quicksort(nums, low, pivot_idx-1, k_small)
        else:
            return 
    
    def partition(self, nums, low, high):
        pivot = nums[high]
        i = low
        for idx in range(low, high):
            if nums[idx] < pivot:
                nums[i], nums[idx] = nums[idx], nums[i]
                i += 1
        nums[i], nums[high] = nums[high], nums[i]
        return i
```

#### 973. K Closest Points to Origin

```python
class Solution:
    def kClosest(self, points: List[List[int]], K: int) -> List[List[int]]:
        heap = []
        for idx in range(K):
            heapq.heappush(heap, (-(points[idx][0]**2+points[idx][1]**2), points[idx]))
        for idx in range(K, len(points)):
            heapq.heappushpop(heap, (-(points[idx][0]**2+points[idx][1]**2), points[idx]))
        return [heapq.heappop(heap)[1] for i in range(K)]
```

#### 347. Top K Frequent Elements

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        nums_dict = {}
        for num in nums:
            if num not in nums_dict:
                nums_dict[num] = 1
            else: nums_dict[num] += 1
        
        return [num[0] for num in heapq.nlargest(k, nums_dict.items(), key=lambda x: x[1])]
```

#### 23. Merge k Sorted Lists

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        heap = []
        for llist in lists:
            while llist:
                heapq.heappush(heap, llist.val)
                llist = llist.next

        dummy = ListNode(None)
        p = dummy
        while heap:
            p.next = ListNode(heapq.heappop(heap))
            p = p.next
        return dummy.next
```

#### 253. Meeting Rooms II

```python
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        n = len(intervals)
        intervals = heapq.nsmallest(n, intervals, key=lambda x: x[0])
        ans = []
        for interval in intervals:
            if not ans: ans.append(interval)
            else:
                signed = 0
                for room in ans:
                    if interval[0]>=room[1]:
                        room[1] = interval[1]
                        signed = 1
                        break
                if not signed: ans.append(interval)
        return len(ans)
```

#### 295. Find Median from Data Stream

```python
class MedianFinder:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.large = []
        self.small = []

    def addNum(self, num: int) -> None:
        if len(self.large) == len(self.small):
            heapq.heappush(self.small, -heapq.heappushpop(self.large, num))
        else:
            heapq.heappush(self.large, -heapq.heappushpop(self.small, -num))

    def findMedian(self) -> float:
        if len(self.large) == len(self.small):
            return (-self.small[0]+self.large[0])/2
        else:
            return -self.small[0]


# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```

### Trie

#### 211. Add and Search Word - Data structure design

```python
class TrieNode:
    def __init__(self):
        self.isWord = False
        self.children = {}

class WordDictionary:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()

    def addWord(self, word: str) -> None:
        """
        Adds a word into the data structure.
        """
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.isWord = True
        

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
        """
        node = self.root
        return self.dfs(word, node)
    
    def dfs(self, word, node):
        if len(word) == 0:
            if node.isWord: return True
            else: return False
        if word[0] == '.':
            flag = False
            for char in node.children.keys():
                flag = (flag or self.dfs(word[1:], node.children[char]))
            return flag
        elif word[0] not in node.children: return False
        else:
            return self.dfs(word[1:], node.children[word[0]])

# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```

#### 208. Implement Trie (Prefix Tree)

```python
class TrieNode:
    def __init__(self):
        self.isWord = False
        self.children = {}

class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()
        

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.isWord = True


    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        node = self.root
        for char in word:
            if char not in node.children: return False
            node = node.children[char]
        return node.isWord
        

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        node = self.root
        for char in prefix:
            if char not in node.children: return False
            node = node.children[char]
        return True

# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

#### 212. Word Search II

```python 
class TrieNode:
    def __init__(self):
        self.isWord = False
        self.children = {}


class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        self.ans = set()
        if not board or not board[0]: return ans

        trie_root = TrieNode()
        for word in words:
            self.add(word, trie_root)

        for i,row in enumerate(board):
            for j,ele in enumerate(row):
                if ele in trie_root.children:
                    temp, board[i][j] = board[i][j], False
                    search = self.dfs(trie_root.children[ele], i, j, board)
                    board[i][j] = temp
                    if search: continue

        return list(self.ans)

    def add(self, word, root):
        node = root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.isWord = word

    def dfs(self, word_node, x, y, board):
        flag = False
        if word_node.isWord:
            self.ans.add(word_node.isWord)
            flag = True
        top, left, bottom, right = False, False, False, False
        if x>0 and board[x-1][y] and board[x-1][y] in word_node.children:
            temp, board[x-1][y] = board[x-1][y], False
            top = self.dfs(word_node.children[temp], x-1, y, board)
            board[x-1][y] = temp
        if y>0 and board[x][y-1] and board[x][y-1] in word_node.children:
            temp, board[x][y-1] = board[x][y-1], False
            left = self.dfs(word_node.children[temp], x, y-1, board)
            board[x][y-1] = temp
        if x<len(board)-1 and board[x+1][y] and board[x+1][y] in word_node.children:
            temp, board[x+1][y] = board[x+1][y], False
            bottom = self.dfs(word_node.children[temp], x+1, y, board)
            board[x+1][y] = temp
        if y<len(board[0])-1 and board[x][y+1] and board[x][y+1] in word_node.children:
            temp, board[x][y+1] = board[x][y+1], False
            right = self.dfs(word_node.children[temp], x, y+1, board)
            board[x][y+1] = temp
        return (flag or top or left or bottom or right)
```

