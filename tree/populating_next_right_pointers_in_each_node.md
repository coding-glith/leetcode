# Populating Next Right Pointers in Each Node

> Given a binary tree

> ```
    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }
```

> Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

> Initially, all next pointers are set to NULL.

> Note:

> * You may only use constant extra space.

> * You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).

> For example,

> Given the following perfect binary tree,

> ```
         1
       /  \
      2    3
     / \  / \
    4  5  6  7
```

> After calling your function, the tree should look like:

> ```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL
```

```Python
# Definition for binary tree with next pointer.
# class TreeLinkNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
#         self.next = None

class Solution(object):
    def connect(self, root):
        """
        :type root: TreeLinkNode
        :rtype: nothing
        """
        if root == None:
            return
        currentNode = root
        nextLevel = None
        while currentNode.left:
            nextLevel = currentNode.left
            while currentNode:
                currentNode.left.next = currentNode.right
                if currentNode.next:
                    currentNode.right.next = currentNode.next.left
                currentNode = currentNode.next
            currentNode = nextLevel
```

```Python
# Definition for binary tree with next pointer.
# class TreeLinkNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
#         self.next = None

class Solution:
    # @param root, a tree link node
    # @return nothing
    def connect(self, root):
        if not root: return root
        root.next = None
        self.popNext(root)

    def popNext(self, root):
        if not root: return
        if not root.left and not root.right: return
        root.left.next = root.right
        root.right.next = root.next.left if root.next else None
        self.popNext(root.left)
        self.popNext(root.right)
```

# Populating Next Right Pointers in Each Node II

> Follow up for problem "Populating Next Right Pointers in Each Node".

> What if the given tree could be any binary tree? Would your previous solution still work?

> Note:

> * You may only use constant extra space.

> For example,

> Given the following binary tree,

> ```
         1
       /  \
      2    3
     / \    \
    4   5    7
```

> After calling your function, the tree should look like:

> ```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL
```

The idea is to use a function called popNext() to help get the nextNode in the same level and itsChild. Moreover, when moving to the next level, popNext() helps to check if the node is a leaf, if yes, it will check its next neighbor otherwise return None and finish the loop.

```Python
# Definition for binary tree with next pointer.
# class TreeLinkNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
#         self.next = None

class Solution(object):
    def connect(self, root):
        """
        :type root: TreeLinkNode
        :rtype: nothing
        """
        if root == None:
            return
        currentNode = root
        prevNode = currentNode  # prevNode stores the leftmost node at a level
        while currentNode:
            nextNode, itsChild = self.popNext(currentNode.next)
            if currentNode.left:
                currentNode.left.next = currentNode.right if currentNode.right else itsChild
            if currentNode.right:
                currentNode.right.next = itsChild
            if nextNode:  # in case currentNode changes, prevNode will help
                currentNode = nextNode
            else:   # move to the next level
                currentNode = prevNode.left if prevNode.left else prevNode.right
                currentNode, _ = self.popNext(currentNode)  # in case currentNode is a leaf
                prevNode = currentNode
    
    def popNext(self, root):
        # this function is to return the node at the same level
        # and its available child
        while root:
            if root.left:
                return root, root.left
            if root.right:
                return root, root.right
            root = root.next
        return None, None
```

Donot understand why following code cannot pass oj.

```Python
# Definition for binary tree with next pointer.
# class TreeLinkNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
#         self.next = None

class Solution:
    # @param root, a tree link node
    # @return nothing
    def connect(self, root):
        if not root: return
        root.next = None
        self.popNext(root)
    
    def popNext(self, root):
        if not root: return
        if not root.left and not root.right: return
        if root.left:
            root.left.next = self.available(root, 0)
        if root.right:
            root.right.next = self.available(root, 1)
        self.popNext(root.left)
        self.popNext(root.right)
    
    def available(self, root, flag):
        if not root: return None
        if flag == 0 and root.right:
            return root.right
        if root.next:
            if root.next.left: return root.next.left
            else: return self.available(root.next, 0)
        return None
```
