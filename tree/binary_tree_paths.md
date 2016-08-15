# Binary Tree Paths

> Given a binary tree, return all root-to-leaf paths.

> For example, given the following binary tree:

> ```
   1
 /   \
2     3
 \
  5
```

> All root-to-leaf paths are:

> ```
["1->2->5", "1->3"]
```

```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    # @param {TreeNode} root
    # @return {string[]}
    def binaryTreePaths(self, root):
        result = []
        if not root:
            return []
        if not root.left and not root.right:
            return [str(root.val)]
        left = self.binaryTreePaths(root.left)
        right = self.binaryTreePaths(root.right)
        allPaths = left + right
        return ['%s->%s' % (root.val, path) for path in allPaths]
```
