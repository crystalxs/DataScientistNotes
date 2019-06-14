# Linked list

## Methods

### Dummy Node

> Add dummy node at the head.

```python
Dummy = ListNode()
```

**When to use dummy node:** when linked list's structure changed.

**Do I need to delete dummy node:** no.

**Does dummy node calculated as extract space:** no.

### Reverse Linked List

1. Create dummy node `head` before start node.

2. Keep 2 pointer `prev` and `curt`,

3. Revert

   ```python
   while (curt != None):
       temp = curt.next
       curt.next = prev
       prev = curt
       curt = temp
   ```

### Multi Pointer

> Multi-pointers with different speed or one begin first.

* Find the end of list.
* Find the number of nodes in list cycle.

## Questions Classify

- Reverse
- Merge
- Search
- Sort (Partition)

## Attention

- Boundary Check
  - `head.next.next` will raise error if `head.next` is not exist
- Length Check
  - Length = 0: `head`
  - Length = 1: `head.next`
  - recheck after one reverse
- Cycle Check
- Operation order does matter
- Don't know the list length
- **Python specific attention**
  - Start index 1

## Leetcode

### Cycle

#### 141. Linked list cycle

> fast and slow pointers

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        pf = head
        ps = head
        while pf:
            try:
                pf = pf.next.next
            except:
                return False
            ps = ps.next
            if pf==ps:
                return True
        return False
```

### Reverse

#### 206. Reverse Linked List

> iteration or recursive

- recursive: `head.next.next = head`; `head.next = None`

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        # iteration
        # if not head:
        #     self.ans = None
        #     return self.ans
        # self.ans = ListNode(head.val)
        # while head.next:
        #     head = head.next
        #     tmp = ListNode(head.val)
        #     tmp.next=self.ans
        #     self.ans=tmp
        # return self.ans
        if not head or not head.next:
            return head
        tmp = self.reverseList(head.next)
        head.next.next=head
        head.next=None
        return tmp
```

#### 25. Reverse Nodes in k-Group

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseKGroup(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if not head or not head.next: return head
        if k < 2: return head
        # 2 pointer
        # 1 go for k step
        # if break return head, length < k
        dummy = ListNode(None)
        dummy.next = head
        fhead = dummy
        
        i = 0
        pre, pf = dummy, head
        while i<=k:
            if i == k: # pass k node
                # print(fhead.val, fhead.next.val, pre.val, pf.val)
                i = 0
                fhead.next, fhead = self.reverseGroup(fhead.next, pre)
                fhead.next = pf
            i += 1
            if not pf: break
            pre, pf = pf, pf.next
        return dummy.next
             
    def reverseGroup(self, head, end):
        # return head and end
        eend = head
        head.next, head, pre, post = None, head.next, head, head.next
        while pre != end:
            head.next, head, pre, post = pre, head.next, head, head.next
            # print("pre", pre.val)
        return pre, eend
```

#### 24. Swap nodes in pairs

> recursive

- `tmp = head.next.next`
- `head.next.next = head`
- `head.next = recursive return`
- `return head.next`

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head
        p = head.next
        tmp = p.next
        p.next = head
        head.next = self.swapPairs(tmp)
        return p
```

#### 143. Reorder List

> fast and slow point & reverse list

- pointer find mid
- reverse list left half then right half

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: None Do not return anything, modify head in-place instead.
        """
        if not head or not head.next: return
        pf = head
        ps = head
        while ps and ps.next:
            ps=ps.next.next
            pf=pf.next #pf=n//2+1
            
        pre, pf.next, pf = None, None, pf.next
        while pf:
            pf.next, pre, pf = pre, pf, pf.next
        while head and pre:
            head.next, head, pre.next, pre = pre, head.next, head.next, pre.next
            

        # pre, pf.next, pf = None, None, pf.next
            # head.next, head, pre.next, pre = pre, head.next, head.next, pre.next 
```

#### 61. Rotate List

> 2 pointers (refer 19.)

- avoid multi loop, record list length if possible
- attention to multi exit points

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def rotateRight(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if not head or not head.next: return head
        if k == 0: return head
        pf, ps = head, head
        dummy = ListNode(None)
        dummy.next = head
        n = 0
        while k>0:
            if not pf: 
                # if link list length smaller than k, restart from head
                pf = head 
                k = k%n
                if k == 0: return head
                continue
            n += 1
            pf = pf.next
            k -= 1 
        if not pf: return head
        while pf.next:
            pf, ps = pf.next, ps.next
        dummy.next = ps.next
        pf.next = head
        ps.next = None
        return dummy.next
```

#### 

### Merge

#### 21. Merge Two Sorted Lists

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummy = ListNode(0)
        head = dummy
        while l1 and l2:
            # print(l1.val, l2.val)
            if l1.val < l2.val:
                current = ListNode(l1.val)
                head.next, head = l1, l1
                l1.next, l1 = None, l1.next
            else:
                current = ListNode(l2.val)
                head.next, head = l2, l2
                l2.next, l2 = None, l2.next
        # print(l1, l2, head.val)
        if l1: head.next = l1
        if l2: head.next = l2
        return dummy.next
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
        dummy = ListNode(None)
        p = dummy
        compared = []
        for llist in lists:
            if llist: compared.append((llist.val, llist.next))
        # print(compared)
        while compared:
            minVal = min(compared, key=lambda x:x[0])
            minVal, nextNode = compared[compared.index(minVal)]
            compared.remove((minVal, nextNode))
            if nextNode: compared.append((nextNode.val,nextNode.next))
            p.next = ListNode(minVal)
            p = p.next
        return dummy.next
```

### Search

#### 19. Remove Nth Node From End of List

> 2 pointers

- first pointer goes n+1 step before
- when first pointer when to end, the second pointer's next node is the removed node

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        pf = head
        ps = head
        while n>0:
            if not pf: return head
            pf = pf.next
            n -= 1
        # calculate ll length
        if not pf: return head.next
        pf=pf.next
        while pf:
            pf = pf.next
            ps = ps.next
        ps.next = ps.next.next
        return head
```

#### 82. Remove Duplicates from Sorted List II

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next: return head
        fnode = ListNode(None)
        fnode.next = head
        p1 = fnode
        p2 = fnode.next
        tmp = None
        while p2:
            if p2.next and p2.val == p2.next.val:
                p1.next = p2.next.next
                tmp = p2.val
                p2=p2.next.next
            elif p2.val == tmp:
                p1.next = p2.next
                p2 = p2.next
            else:
                p2=p2.next
                p1=p1.next
        return fnode.next
```

#### 147. Insertion Sort List

Tag: linked list, insertion sort

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next: return head
        dummy = ListNode(None)
        dummy.next = head
        p = head
        pre, p.next, p = p, None, p.next
        while p:
            post = p.next
            dummy.next, pre = self.insert(dummy.next, pre, p)
            p = post
        return dummy.next
    
    def insert(self, head, end, node):
        # head.length >= 1
        dummy = ListNode(None)
        dummy.next = head
        p = dummy
        while p.next:
            if p.next.val <= node.val:
                p = p.next
                if not p.next: 
                    p.next = node
                    node.next = None
                    end = node
                    break
            else:
                p.next, node.next = node, p.next
                break
        return dummy.next, end
```

### Partition

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

#### 86. Partition List

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        if not head or not head.next: return head
        dummy = ListNode(None)
        dummy.next = head
        p1, p2, p2pre= dummy, head, dummy
        first = True
        while p2:
            if p2.val < x:
                p1.next = p2
                p1 = p1.next
                p2 = p2.next
                if not first: p1.next = p2head
                if p2pre != dummy: p2pre.next = p2
            else:
                if first: 
                    p2head = p2
                    first = False
                p2pre = p2
                p2 = p2.next
        return dummy.next
```





#### 2. Add two numbers

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def sum(self, num1, num2):
        if num1+num2>9:
            return 1, num1+num2-10
        else: return 0, num1+num2
        
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        carry, value = self.sum(l1.val, l2.val)
        self.ans = ListNode(value)
        current = self.ans
        while l1.next != None or l2.next != None or carry ==1:
            if l1.next == None and l2.next == None and carry == 1:
                current.next = ListNode(1)
                break
            elif l1.next == None and l2.next != None:
                l2 = l2.next
                if l2.val == 9 and carry == 1:
                    current.next = ListNode(0)
                    carry = 1
                else: 
                    current.next = ListNode(l2.val+carry)
                    carry = 0
                current = current.next
            elif l1.next != None and l2.next == None:
                l1 = l1.next
                if l1.val == 9 and carry == 1:
                    current.next = ListNode(0)
                    carry = 1
                else:
                    current.next = ListNode(l1.val+carry)
                    carry = 0
                current = current.next
            else:
                l1 = l1.next
                l2 = l2.next
                carry, value = self.sum(l1.val, l2.val+carry)
                current.next = ListNode(value)
                current = current.next
        return self.ans
```

#### 234. Palindrome linked list

> fast and slow pointer

- fast pointer arrive mean slow pointer arrive mid
- reverse first half

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        pf = head
        ps = head
        reverse = head
        new = None
        if not head or not head.next: return True
        while True:
            if not pf.next: 
                reverse = new.next
                ps = ps.next
                break
            pf = pf.next.next
            ps = ps.next
            if new: reverse.next = new.next
            if not pf: break
            new = ListNode(ps.val)
            new.next = reverse
            reverse = ps
        head.next = None
        while ps:
            if ps.val != reverse.val: return False
            ps = ps.next
            reverse = reverse.next
        return True
```

#### 138. Copy List with Random Pointer

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val, next, random):
        self.val = val
        self.next = next
        self.random = random
"""
class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        dummy = Node(0, None, None)
        list_map = {}
        new_head = dummy
        old_head = head
        while old_head:
            current = Node(old_head.val, None, None)
            new_head.next = current
            new_head = new_head.next
            list_map[old_head] = new_head
            old_head = old_head.next
        
        old_head = head
        new_head = dummy.next
        while old_head:
            if old_head.random:
                new_head.random = list_map[old_head.random]
            new_head = new_head.next
            old_head = old_head.next
        return dummy.next
```

