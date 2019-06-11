# Tree

## Methods

### DFS

#### Recursive

```python
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        self.ans = self.dfs(root)
        return self.ans
    
    def dfs(self, p:TreeNode):
      	ans = []
        if p is None: return ans
        ans.append(p.val) # preorder
        ans.extend(self.dfs(p.left))
        # ans.append(p.val) # inorder
        ans.extend(self.dfs(p.right))
        # ans.append(p.val) # postorder
        return ans
```

#### Stack

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        self.ans = []
        stack = []
        p = root
        while p or len(stack)!=0:
            while p:
                # self.ans.append(p.val) # preorder
                stack.append(p)
                p = p.left
            p = stack.pop()
            self.ans.append(p.val) # inorder
            p = p.right
            # self.ans.append(p.val) # postorder
        return self.ans
```

### Level order <a name="level-order"/>

#### Recursive

```python
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        self.ans ={}
        self.dfs(root, 1)
        return self.ans.values()
        
        
    def dfs(self, root, depth):
        if not root: return
        if depth not in self.ans:
            self.ans[depth] = []
        self.ans[depth].append(root.val)
        self.dfs(root.left, depth+1)
        self.dfs(root.right, depth+1)
```

#### Queue

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        self.ans = []
        if not root: return []
        
        # 1. create a queue, and put root node into it
        queue = []
        queue.append(root)
        
        # 2. while queue is not empty
        while queue:
            currentLevel = []
            n = len(queue)
            while n>0:
                node = queue.pop(0)
                currentLevel.append(node.val)
                if node.left: queue.append(node.left)
                if node.right: queue.append(node.right)
                n -= 1
            self.ans.append(currentLevel)
        return self.ans
```

## Questions Classify

### Traverse

* Preorde/inorder/postorder: dfs
* Level order: bfs

### Serialization

> Transfer object to string.

Use breadth first search. See [297. Serialize and Deserialize Binary Tree](../DS/Btree.md/#297)

##Attention

- Condition check is lazy, don't put recursion under conditions, sometimes it will skip the part after `and` / `or`.

##Leetcode

### Traverse (DFS)

#### 94. Binary Tree Inorder Traversal

##### Iteration

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        self.ans = []
        stack = []
        p = root
        while p or len(stack)!=0:
            while p:
                stack.append(p)
                p = p.left
            p = stack.pop()
            self.ans.append(p.val)
            p = p.right
        return self.ans
```

#### 144. Binary Tree Preorder Traversal

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        self.ans = []
        
        self.dfs(root)
        return self.ans
    
    def dfs(self, p:TreeNode):
        if p is None: return
        self.ans.append(p.val)
        self.dfs(p.left)
        self.dfs(p.right)
```

#### 145. Binary Tree Postorder Traversal

##### Recursive

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        self.ans = []
        
        self.dfs(root)
        return self.ans
    
    def dfs(self, p:TreeNode):
        if p is None: return
        self.dfs(p.left)
        self.dfs(p.right)
        self.ans.append(p.val)
```

##### Iteration

* reverse of preorder from right to left

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        self.ans = []
        if not root: return self.ans
        
        stack = []
        pointer = root
        while pointer or stack:
            while pointer:
                self.ans.append(pointer.val)
                stack.append(pointer)
                pointer = pointer.right
            pointer = stack.pop()
            pointer = pointer.left
        return self.ans[::-1]
```

#### 226. Invert Binary Tree

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if not root: return root
        return self.inverttree(root)
        
    def inverttree(self, root):
        root.left, root.right = root.right, root.left
        if root.left: root.left = self.inverttree(root.left)
        if root.right: root.right = self.inverttree(root.right)
        return root
        
```

#### 100. Same Tree

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def __init__(self):
        self.ans = True
        
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """
        if p is None and q is None: return self.ans
        elif p is None or q is None:
            self.ans = False
        elif p.val !=  q.val:
            self.ans = False
        else:
            self.isSameTree(p.left,q.left)
            self.isSameTree(p.right, q.right)
        return self.ans
```

#### 101. Symmetric Tree

##### Iteration

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root: return True
        lstack = []
        rstack = []
        lp, rp = root, root
        while lp or rp or len(lstack)>0 or len(rstack)>0:
            while lp and rp:
                if lp.val != rp.val: return False
                lstack.append(lp)
                rstack.append(rp)
                lp = lp.left
                rp = rp.right
            if not lp and not rp:
                lp = lstack.pop()
                lp = lp.right
                rp = rstack.pop()
                rp = rp.left
            else: return False
        return True
```

##### Recursive

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        self.ans = True
        if not root: return self.ans
        self.isSymmetricNode(root.left, root.right)
        return self.ans
        
    def isSymmetricNode(self, left, right):
        if not left and not right: return
        if not left or not right:
            self.ans = False
            return
        if left.val != right.val:
            self.ans = False
            return
        else:
            self.isSymmetricNode(left.left, right.right)
            self.isSymmetricNode(left.right, right.left)
```

#### 129. Sum Root to Leaf Numbers

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sumNumbers(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        self.num = []
        self.findNumber(root,0)
        return sum(self.num)
        
    def findNumber(self, root, num):
        # end case
        if not root: return
        if not root.left and not root.right: 
            self.num.append(num*10+root.val)
            return
        self.findNumber(root.left,num*10+root.val)
        self.findNumber(root.right,num*10+root.val)
```

#### 110. Balanced Binary Tree

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        self.ans = True
        if not root: return self.ans
        left_depth = self.dfs(root.left)
        right_depth = self.dfs(root.right)
        if self.ans and abs(left_depth-right_depth)<2:
            return self.ans
        else: return False
        
    def dfs(self, root):
        if not root: return 0
        left_depth = self.dfs(root.left)
        right_depth = self.dfs(root.right)
        if abs(left_depth-right_depth)>1: self.ans=False
        return max(left_depth, right_depth)+1
```

#### 113. Path Sum II

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
        if not root: return []
        self.ans = []
        
        self.dfs(root, self.ans, sum, [])
        return self.ans
    
    def dfs(self, node, ans_lists, sum, pre_list):
        current_list = pre_list+[node.val]
        if not node.left and not node.right:
            if sum-node.val == 0: ans_lists.append(current_list)
            return
        if node.left: self.dfs(node.left, ans_lists, sum-node.val, current_list)
        if node.right: self.dfs(node.right, ans_lists, sum-node.val, current_list)
```

#### 112. Path Sum

```python
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        self.ans = False
        if not root: return self.ans
        stack = []
        while root:
            # print(root.val, sum)
            if root.val == sum:
                if not root.left and not root.right:
                    self.ans = True
                    return self.ans
                else:
                    sum -= root.val
                    if root.left: stack.append((root.left,sum))
                    if root.right: stack.append((root.right,sum))
            else:
                sum -= root.val
                # print(root.val, sum)
                if root.left: stack.append((root.left,sum))
                if root.right: stack.append((root.right,sum))
            if len(stack) == 0: break
            root, sum = stack.pop(0)
            
        return self.ans
```

#### 24. Binary Tree Maximum Path Sum

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxPathSum(self, root: TreeNode) -> int:
        if not root: return 0
        self.ans = root.val
        max_sum = {}
        self.dfs(root, max_sum)
        return self.ans
    
    def dfs(self, root, max_sum):
        max_sum[root] = root.val
        if root.left:
            self.dfs(root.left, max_sum)
            if max_sum[root.left]>0: max_sum[root] += max_sum[root.left]
        if root.right:
            self.dfs(root.right, max_sum)
            if max_sum[root.right]>0: max_sum[root] += max_sum[root.right]
        if max_sum[root] > self.ans:
            self.ans = max_sum[root]
        if root.left and root.right and max_sum[root.left]>0 and max_sum[root.right]>0:
            if max_sum[root.left]>max_sum[root.right]: max_sum[root] -= max_sum[root.right]
            else: max_sum[root] -= max_sum[root.left]
```

#### 98. Validate Binary Search Tree

> Inorder ascending

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        if not root: return True
        ans = []
        pointer = root
        stack = []
        while pointer or len(stack)!=0:
            while pointer:
                stack.append(pointer)
                pointer = pointer.left
            pointer = stack.pop()
            if ans:
                if pointer.val <= ans[-1]: return False
            ans.append(pointer.val)
            pointer = pointer.right
        return True
```

#### 250. Count Univalue Subtrees

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def countUnivalSubtrees(self, root: TreeNode) -> int:
        if not root: return 0
        self.ans = 0
        self.dfs(root)
        return self.ans
    
    def dfs(self, node):
        if not node: return True
        left = self.dfs(node.left)
        right = self.dfs(node.right)
        if left and right:
            if node.left and node.left.val != node.val: return False
            if node.right and node.right.val != node.val: return False
            self.ans += 1
            return True
```

#### 104. Maximum Depth of Binary Tree

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        self.ans = 0
        if not root: return self.ans
        self.dfs(root, 0)
        return self.ans
        
    def dfs(self, root, depth):
        if root is None:
            if depth > self.ans: self.ans = depth
            return
        self.dfs(root.left, depth+1)
        self.dfs(root.right, depth+1)
```

#### 366. Find Leaves of Binary Tree

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def findLeaves(self, root: TreeNode) -> List[List[int]]:
        if not root: return []
        ans = {}
        self.leaves(root, ans)
        ans = sorted(ans.items(), key = lambda x: x[0])
        return [level[1] for level in ans]
    
    def leaves(self, node, ans):
        if not node: return 0
        left_depth = self.leaves(node.left, ans)
        right_depth = self.leaves(node.right, ans)
        depth = max(left_depth+1, right_depth+1)
        if depth in ans:
            ans[depth].append(node.val)
        else:
            ans[depth] = [node.val]
        return depth
```

#### 236. Lowest Common Ancestor of a Binary Tree

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if not root: return root
        self.ans = []
        self.dfs(root, p, q)
        # print(self.ans)
        return self.ans[0]
    
    def dfs(self, node, p, q):
        if not node: return False
        left = self.dfs(node.left, p, q)
        right = self.dfs(node.right, p, q)
        this = (node == p or node == q)
        # print(node.val, left, right, this)
        if left + right + this > 1:
            self.ans.append(node)
        return left or right or this
```

### BFS

#### 102. Binary Tree Level Order Traversal

##### DFS

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        self.ans ={}
        self.dfs(root, 1)
        return self.ans.values()
        
        
    def dfs(self, root, depth):
        if not root: return
        if depth not in self.ans:
            self.ans[depth] = []
        self.ans[depth].append(root.val)
        self.dfs(root.left, depth+1)
        self.dfs(root.right, depth+1)
```

##### Queue

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        self.ans = []
        if not root: return []
        
        # 1. create a queue, and put root node into it
        queue = []
        queue.append(root)
        
        # 2. while queue is not empty
        while queue:
            currentLevel = []
            n = len(queue)
            while n>0:
                node = queue.pop(0)
                currentLevel.append(node.val)
                if node.left: queue.append(node.left)
                if node.right: queue.append(node.right)
                n -= 1
            self.ans.append(currentLevel)
        return self.ans
```

#### 103. Binary Tree Zigzag Level Order Traversal

1. [102. Binary Tree Level Order Traversal](#102. Binary Tree Level Order Traversal)
2. reverse the even num rows

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def zigzagLevelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        self.ans = {}
        self.dfs(root, 1)
        if len(self.ans.values()) > 0:
            for nodes in self.ans.values()[1::2]:
                nodes.reverse()
        return self.ans.values()
        
    def dfs(self, root, depth):
        if not root: return
        if depth not in self.ans: self.ans[depth] = []
        self.ans[depth].append(root.val)
        self.dfs(root.left, depth+1)
        self.dfs(root.right, depth+1)
```

#### 199. Binary Tree Right Side View

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def rightSideView(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        self.ans = {}
        stack = []
        depth = 0
        while root or len(stack) != 0:
            while root:
                depth += 1
                stack.append((depth,root))
                root = root.right
            pair = stack.pop()
            depth, root = pair[0], pair[1]
            if depth not in self.ans: self.ans[depth] = root.val
            root = root.left
        return self.ans.values()  
```

## Others

#### 230. Kth Smallest Element in a BST

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def kthSmallest(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: int
        """
        p = root
        stack = []
        while p or len(stack)!=0:
            while p:
                stack.append(p)
                p = p.left
            p = stack.pop()
            k -= 1
            if k == 0: break
            p = p.right
        return p.val
```

#### 173. Binary Search Tree Iterator

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class BSTIterator(object):

    def __init__(self, root):
        """
        :type root: TreeNode
        """
        self.root = root
        self.list = []
        self.inorder()
        
    def inorder(self):
        stack = []
        while self.root or len(stack)>0:
            while self.root:
                stack.append(self.root)
                self.root = self.root.left
            self.root = stack.pop()
            self.list.append(self.root.val)
            self.root = self.root.right

    def next(self):
        """
        @return the next smallest number
        :rtype: int
        """
        return self.list.pop(0)
            
    def hasNext(self):
        """
        @return whether we have a next smallest number
        :rtype: bool
        """
        if len(self.list)>0: return True
        else: return False
```

### 114. Flatten Binary Tree to Linked List

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: None Do not return anything, modify root in-place instead.
        """
        stack = []
        while root or len(stack)>0:
            while root:
                if root.right: stack.append(root.right)
                if root.left:
                    root.right = root.left
                    root.left,root = None, root.left
                else: break
            if len(stack)==0: break
            root.right = stack.pop()
            root = root.right
            
```

### 297. Serialize and Deserialize Binary Tree <a name="297"/>

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        output = []
        queue = []
        if not root: return output
        
        queue.append(root)
        while queue:
            current = queue.pop(0)
            if not current: output.append(None)
            else:
                output.append(current.val)
                queue.append(current.left)
                queue.append(current.right)
        return output
        
        
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if not data: return
        queue = []
        root = TreeNode(data.pop(0))
        queue.append(root)
        while data and queue:
            currentRoot = queue.pop(0)
            currentLeft = data.pop(0)
            # print(currentLeft)
            if currentLeft is not None:
                currentLeftNode = TreeNode(currentLeft)
                queue.append(currentLeftNode)
                currentRoot.left = currentLeftNode
                # print(currentRoot.left.val)
            currentRight = data.pop(0)
            # print(currentRight)
            if currentRight is not None:
                currentRightNode = TreeNode(currentRight)
                queue.append(currentRightNode)
                currentRoot.right = currentRightNode
        return root
        
        
# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```

