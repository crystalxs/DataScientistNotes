# Linked list

#### Methods

- Multi-pointers with different speed or one begin first.
- Add dummy node at the head.
  - How to use dummy node
  - When to use dummy node?
  - head = dummy 这句话总是需要么?
  - Dummy Node 是否需要删除?
  - 使用 Dummy Node 算面试官会说我耗费了额外空间么?
  - Dummy Node 非用不可么?
  - Dummy Node 初始化的值重要么?
  - 链表的问题都需要用到 Dummy Node 么?

#### Questions Classify

- reverse
- find k in the end
- sort

#### Attention

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

206. **Reverse Linked List:** iteration or recursive
     - recursive: `head.next.next = head`; `head.next = None`
207. **Linked list cycle:** fast and slow pointers
208. **Swap nodes in pairs:** recursive
     - `tmp = head.next.next`
     - `head.next.next = head`
     - `head.next = recursive return`
     - `return head.next`
209. **Add two numbers:**
210. **Palindrome linked list:** fast and slow pointer
     - fast pointer arrive mean slow pointer arrive mid
     - reverse first half
211. **Remove n-th node from end of list:** 2 pointers
     - first pointer goes n+1 step before
     - when first pointer when to end, the second pointer's next node is the removed node
212. **Reorder List:** fast and slow point & reverse list
     - pointer find mid
     - reverse list left half then right half
213. **Rotate List:** 2 pointers (refer 19.)
     - avoid multi loop, record list length if possible
     - attention to multi exit points

#### 19. Remove Nth Node from end of list

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

#### 24. Swap nodes in pairs

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

#### 25.

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
        head.next, head, pre, post, = None, head.next, head, head.next
        while pre != end:
            head.next, head, pre, post = pre, head.next, head, head.next
            # print("pre", pre.val)
        return pre, eend
```

#### 61.

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