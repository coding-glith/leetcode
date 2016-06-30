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
