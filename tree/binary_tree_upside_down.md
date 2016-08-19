# Binary Tree Upside Down

> Given a binary tree where all the right nodes are either leaf nodes with a sibling (a left node that shares the same parent node) or empty, flip it upside down and turn it into a tree where the original right nodes turned into left leaf nodes. Return the new root.

> For example:

> Given a binary tree {1,2,3,4,5},

> ```
    1
   / \
  2   3
 / \
4   5
```

> return the root of the binary tree [4,5,2,#,#,3,1].

> ```
   4
  / \
 5   2
    / \
   3   1  
```

Iterative Solution.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def upsideDownBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        prev, prevRight = None, None
        while root:
            root.right, root.left, prev, prevRight, root = prev, prevRight, root, root.right, root.left
        return prev
```

Recursive solution. Don't quite understand yet. :-(

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def upsideDownBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if not root or (not root.left and not root.right):
            return root
        left = self.upsideDownBinaryTree(root.left)
        root.left.left = root.right
        root.left.right = root
        root.left = None
        root.right = None
        return left
```
