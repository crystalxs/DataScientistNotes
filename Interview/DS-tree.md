# Tree

## Questions Classify

### Traverse

#### DFS

##### Recursive

```python
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

##### Stack

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

#### Level order <a name="level-order"/>

##### Recursive

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

##### Queue

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

### Serialization

> Transfer object to string.

Use breadth first search. See [297. Serialize and Deserialize Binary Tree](../DS/Btree.md/#297)

## Methods

- Recursive
- Iteration with stack/queue

##Attention

- 

##Leetcode

199. Binary Tree Right Side View [tree]
200. Invert Binary Tree [tree]
201. Kth Smallest Element in a BST [bst]

#### 230. Kth Smallest Element in a BST

Tag: binary search tree / stack application

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

Tag: BST / stack application

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

## Traverse

### 94. Binary Tree Inorder Traversal

#### Iteration

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

#### Recursive

### 144. Binary Tree Preorder Traversal

same as [94. Binary Tree Inorder Traversal](94. Binary Tree Inorder Traversal)

### 145. Binary Tree Postorder Traversal

same as [94. Binary Tree Inorder Traversal](#94. Binary Tree Inorder Traversal)

### 102. Binary Tree Level Order Traversal

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

### 103. Binary Tree Zigzag Level Order Traversal

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

## DFS

### 104. Maximum Depth of Binary Tree

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

### 226. Invert Binary Tree

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

### 100. Same Tree

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

### 101. Symmetric Tree

#### Iteration

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

#### Recursive

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

### 129. Sum Root to Leaf Numbers

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

### 110. Balanced Binary Tree

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

### 113. Path Sum II

1. Same as [112. Path Sum](112. Path Sum)
2. Track the path

### 112. Path Sum

Tag: binary tree / stack

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

### 111. Minimum Depth of Binary Tree

Reverse of [104. Maximum Depth of Binary Tree](104. Maximum Depth of Binary Tree.md)

## BFS

### 199. Binary Tree Right Side View

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

### 107. Binary Tree Level Order Traversal II

Same as [102. Binary Tree Level Order Traversal](#102. Binary Tree Level Order Traversal)

## Others

### [todo] 96. Unique Binary Search Trees

### 114. Flatten Binary Tree to Linked List

Tag: binary tree / in-place / stack application

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

### [todo] 106.

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

