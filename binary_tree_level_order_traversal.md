# Binary Tree Level Order Traversal

> Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

> For example:

> Given binary tree [3,9,20,null,null,15,7],

> ```
    3
   / \
  9  20
    /  \
   15   7
```

> return its level order traversal as:

> ```
[
  [3],
  [9,20],
  [15,7]
]
```

```Python
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
        if root == None:
            return []
        result = []
        self.dfs(root, result, 0)
        return result
    
    def dfs(self, root, result, level):
        if root == None:
            return []
        if len(result) < level + 1:
            result.append([])
        result[level].append(root.val)
        self.dfs(root.left, result, level + 1)
        self.dfs(root.right, result, level + 1)
```

# Binary Tree Level Order Traversal II

> Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

> For example:

> Given binary tree [3,9,20,null,null,15,7],

> ```
    3
   / \
  9  20
    /  \
   15   7
```

> return its bottom-up level order traversal as:

> ```
[
  [15,7],
  [9,20],
  [3]
]
```

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def levelOrderBottom(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if root == None:
            return []
        result = []
        height = self.getHeight(root)
        heightVal = height
        while heightVal > 0:
            result.append([])
            heightVal -= 1
        self.dfs(root, height, result, 0)
        return result
    
    def dfs(self, root, height, result, level):
        if root == None:
            return []
        result[height-level-1].append(root.val)
        self.dfs(root.left, height, result, level + 1)
        self.dfs(root.right, height, result, level + 1)
    
    def getHeight(self, root):
        if root.left == None or root.right == None:
            return 0
        left = self.getHeight(root.left)
        right = self.getHeight(root.right)
        return left + 1 if left > right else right + 1
```