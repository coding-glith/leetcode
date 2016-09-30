# Binary Tree Right Side View

> Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

> For example:

> Given the following binary tree,

> ```
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

> You should return [1, 3, 4].

```Python
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
        res = []
        self.getVal(res, root, 0)
        return res

    def getVal(self, res, root, level):
        if not root:
            return
        if level == len(res):
            res.append(root.val)
        self.getVal(res, root.right, level + 1)
        self.getVal(res, root.left, level + 1)
```

BFS.

```Python
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
        if not root: return []
        res, level = [root.val], [root]
        while level:
            nextLevel = []
            for node in level:
                if node.left: nextLevel.append(node.left)
                if node.right: nextLevel.append(node.right)
            level = nextLevel
            if nextLevel: res.append(nextLevel[-1].val)
        return res
```
