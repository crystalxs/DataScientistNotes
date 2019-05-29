# Tree

## Definitions

> <http://interactivepython.org/courselib/static/pythonds/Trees/VocabularyandDefinitions.html>

##Binary tree

### Implementation

#### List of lists

#### Nodes

A tree with exactly two sub-trees for each node, called the `left` and `right` sub-trees.

```python
class TreeNode:
    def __init__(self, value, left, right):
        self.value = value
        self.left = left
        self.right = right

		def insertLeft(self,newNode):
        if self.leftChild == None:
            self.leftChild = BinaryTree(newNode)
        else:
            t = BinaryTree(newNode)
            t.leftChild = self.leftChild
            self.leftChild = t

		def insertRight(self,newNode):
        if self.rightChild == None:
            self.rightChild = BinaryTree(newNode)
        else:
            t = BinaryTree(newNode)
            t.rightChild = self.rightChild
            self.rightChild = t

    def getRightChild(self):
        return self.rightChild

    def getLeftChild(self):
        return self.leftChild

    def setRootVal(self,obj):
        self.key = obj

    def getRootVal(self):
        return self.key
```

###Traversals

**Preorder**: Compute before visiting nodes

**Inorder:** Compute between visiting left node and right node

**Postorder**: Compute after visiting nodes

####Depth-first Walk 

#####Recursion

```python
def dfs(p:TreeNode):
    if p is None: return
    print(p.value)
    dfs(p.left)
    dfs(p.right)
```

#####Iteration

```python
def dfs(p:TreeNode):
  	stack = []
    while p or len(stack)!=0:
      	while p:
          	stack.append(p)
            p = p.left
        p = stack.pop()
        p = p.right
```

####Breadth-first Walk <a name="bfs"/>

```python
def walk(t:TreeNode) -> int:
    if t is None: return 0
    return t.value + walk(t.left) + walk(t.right)
```

##Binary Search Tree

> A binary tree where, for each node `m`:
>
> * The left sub-tree only has nodes with keys smaller than (according to some total order) the key of `m`;
> * While the right sub-tree only has nodes with keys larger than the key of `m`.

```python
def search_tree(p:TreeNode, value) -> None:
    "add nodes like a binary search tree"
    if value < p.value:
        if p.left is not None: add(p.left, value)
        else: p.left = TreeNode(value)
    if value > p.value:
        if p.right is not None: add(p.right, value)
        else: p.right = TreeNode(value)
    # do nothing if equal (already there)
```

### Restricted Walk

```python
def walk_search_tree(p:TreeNode, x:object):
    if p is None: return None
    if x<p.value:
        return walk_search_tree(p.left, x)
    if x>p.value:
        return walk_search_tree(p.right, x)
    return p
```

## Balanced Binary Tree

> A binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

## Complete Binary Tree

> Each level has all of its nodes;
>
> The exception to this is the bottom level of the tree, which we fill in from left to right.

### Implementation

We can represent it using a single list:

* The left child of a parent (at position p) is the node that is found in position 2p in the list.
* Similarly, the right child of the parent is at position 2p+1 in the list.
* Given that a node is at position n in the list, the parent is at position n/2.

## Balanced Binary Search Tree (AVL Tree)

> A special kind of binary search tree that automatically makes sure that the tree remains balanced at all times. 

### Implementation

> <http://interactivepython.org/courselib/static/pythonds/Trees/AVLTreeImplementation.html>

* Keep track of a balance factor for each node in the tree.

$$
balanceFactor = height(leftSubTree) - height(rightSubTree)
$$

*  A tree to be in balance if the balance factor is -1, 0, or 1.
* Once the balance factor of a node in a tree is outside this range we will need to have a procedure to bring the tree back into balance.
* If the new node is a right child the balance factor of the parent will be reduced by one.
* If the new node is a left child then the balance factor of the parent will be increased by one.
* The recursive call has reached the root of the tree.
* Once a subtree has a balance factor of zero, then the balance of its ancestor nodes does not change.

```python
def _put(self,key,val,currentNode):
    if key < currentNode.key:
        if currentNode.hasLeftChild():
                self._put(key,val,currentNode.leftChild)
        else:
                currentNode.leftChild = TreeNode(key,val,parent=currentNode)
                self.updateBalance(currentNode.leftChild)
    else:
        if currentNode.hasRightChild():
                self._put(key,val,currentNode.rightChild)
        else:
                currentNode.rightChild = TreeNode(key,val,parent=currentNode)
                self.updateBalance(currentNode.rightChild)

def updateBalance(self,node):
    if node.balanceFactor > 1 or node.balanceFactor < -1:
        self.rebalance(node)
        return
    if node.parent != None:
        if node.isLeftChild():
                node.parent.balanceFactor += 1
        elif node.isRightChild():
                node.parent.balanceFactor -= 1

        if node.parent.balanceFactor != 0:
                self.updateBalance(node.parent)
```



### Performance

Searching: $O(logN)$.

## Binary Heap

> When we diagram the heap it looks a lot like a tree, but when we implement it we use only a single list as an internal representation.
>
> **Heap Structure Property**
>
> In a heap, for every node x with parent p, the key in p is smaller than or equal to the key in x.

### Operations

- `BinaryHeap()` creates a new, empty, binary heap.
- `insert(k)` adds a new item to the heap.
- `findMin()` returns the item with the minimum key value, leaving item in the heap.
- `delMin()` returns the item with the minimum key value, removing the item from the heap.
- `isEmpty()` returns true if the heap is empty, false otherwise.
- `size()` returns the number of items in the heap.
- `buildHeap(list)` builds a new heap from a list of keys.

###Min Heap

> The smallest key is always at the front.

####Implementation

* To add an item to a list to maintain the complete tree property and reserve the heap structure property:
  * append the item to the end of the list;
  * if the newly added item is less than its parent, then we can swap the item with its parent until we get to the top of the tree.
* To delete the minimum item in the tree:
  * restore the root item by taking the last item in the list and moving it to the root position;
  * swap the root with its smallest child less than the root.
* To build from a list of keys:
  * 

```python
class BinHeap:
    def __init__(self):
        self.heapList = [0]
        self.currentSize = 0

  def percUp(self,i):
      while i // 2 > 0:
        if self.heapList[i] < self.heapList[i // 2]:
           tmp = self.heapList[i // 2]
           self.heapList[i // 2] = self.heapList[i]
           self.heapList[i] = tmp
        i = i // 2

		def insert(self,k):
        self.heapList.append(k)
        self.currentSize = self.currentSize + 1
        self.percUp(self.currentSize)

  def percDown(self,i):
      while (i * 2) <= self.currentSize:
          mc = self.minChild(i)
          if self.heapList[i] > self.heapList[mc]:
              tmp = self.heapList[i]
              self.heapList[i] = self.heapList[mc]
              self.heapList[mc] = tmp
          i = mc

		def minChild(self,i):
        if i * 2 + 1 > self.currentSize:
            return i * 2
        else:
            if self.heapList[i*2] < self.heapList[i*2+1]:
                return i * 2
            else:
                return i * 2 + 1

    def delMin(self):
        retval = self.heapList[1]
        self.heapList[1] = self.heapList[self.currentSize]
        self.currentSize = self.currentSize - 1
        self.heapList.pop()
        self.percDown(1)
        return retval

		def buildHeap(self,alist):
        i = len(alist) // 2
        self.currentSize = len(alist)
        self.heapList = [0] + alist[:]
        while (i > 0):
            self.percDown(i)
            i = i - 1      
```

###Max Heap

> The largest key value is always at the front.