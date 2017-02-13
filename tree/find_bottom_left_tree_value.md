# Find Bottom Left Tree Value

> Given a binary tree, find the leftmost value in the last row of the tree.

> Example 1:

> ```
Input:
    2
   / \
  1   3
Output:
1
```

> Example 2: 

> ```
Input:
        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7
Output:
7
```

> Note: You may assume the tree (i.e., the given root node) is not NULL.

BFS.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def findBottomLeftValue(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root: return None
        result = root.val
        level = [root]
        while level:
            nextLevel = []
            for node in level:
                if node.left: nextLevel.append(node.left)
                if node.right: nextLevel.append(node.right)
            if nextLevel: result = nextLevel[0].val
            level = nextLevel
        return result
```

DFS.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def findBottomLeftValue(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root: return None
        if not root.left and not root.right: return root.val
        leftLeaf, leftH = self.getLeafHeight(root.left)
        rightLeaf, rightH = self.getLeafHeight(root.right)
        return leftLeaf.val if leftH >= rightH else rightLeaf.val
    
    def getLeafHeight(self, root):
        if not root: return None, 0
        if not root.left and not root.right: return root, 1
        left, leftH = self.getLeafHeight(root.left)
        right, rightH = self.getLeafHeight(root.right)
        if leftH >= rightH:
            return left, leftH + 1
        else:
            return right, rightH + 1
```
