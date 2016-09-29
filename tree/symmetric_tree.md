# Symmetric Tree

> Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

> For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

> ```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

> But the following [1,2,2,null,3,null,3] is not:

> ```
    1
   / \
  2   2
   \   \
   3    3
```

> Note: Bonus points if you could solve it both recursively and iteratively.

Recursive solution:

```Python
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
        if root == None:
            return True
        return self.symTree(root.left, root.right)
            

    def symTree(self, left, right):
        if left == None and right == None:
            return True
        if left == None or right == None:
            return False
        nodeBool = (left.val == right.val)
        leftBool = self.symTree(left.left, right.right)
        rightBool = self.symTree(left.right, right.left)
        return nodeBool and leftBool and rightBool
```

Iterative solution. The idea is to store every node in each level and check the symmetric node's val in the level.

```Python
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
        level = [root]
        while level:
            nextLevel = []
            for i in xrange(len(level)):
                if not level[i] and not level[len(level)-1-i]: continue
                if not level[i] or not level[len(level)-1-i]: return False
                if level[i].val != level[len(level)-1-i].val:
                    return False
                nextLevel.append(level[i].left)
                nextLevel.append(level[i].right)
            level = nextLevel
        return True
```
