# Linked list

#### Methods

* Multi-pointers with different speed or one begin first.

* Add dummy node at the head.
  * How to use dummy node
  * When to use dummy node?
  * head = dummy 这句话总是需要么?
  * Dummy Node 是否需要删除?
  * 使用 Dummy Node 算面试官会说我耗费了额外空间么?
  * Dummy Node 非用不可么?
  * Dummy Node 初始化的值重要么?
  * 链表的问题都需要用到 Dummy Node 么?

#### Questions Classify

* reverse
* find k in the end
* sort

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

#### Leetcode

206. **Reverse Linked List:** iteration or recursive
     * recursive: `head.next.next = head`; `head.next = None`

141. **Linked list cycle:** fast and slow pointers

24. **Swap nodes in pairs:** recursive
    * `tmp = head.next.next`
    * `head.next.next = head`
    * `head.next = recursive return`
    * `return head.next`

2. **Add two numbers:**

234. **Palindrome linked list:** fast and slow pointer
     * fast pointer arrive mean slow pointer arrive mid
     * reverse first half

19. **Remove n-th node from end of list:** 2 pointers
    * first pointer goes n+1 step before
    * when first pointer when to end, the second pointer's next node is the removed node

143. **Reorder List:** fast and slow point & reverse list
     * pointer find mid
     * reverse list left half then right half

61. **Rotate List:** 2 pointers (refer 19.)
    * avoid multi loop, record list length if possible
    * attention to multi exit points