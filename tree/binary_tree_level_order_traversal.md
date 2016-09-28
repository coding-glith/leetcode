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

BFS.

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
        if not root:
            return []
        res, level = [[root.val]], [root]
        while level:
            nextLevel, tmp = [], []
            for node in level:
                if node.left:
                    nextLevel.append(node.left)
                    tmp.append(node.left.val)
                if node.right:
                    nextLevel.append(node.right)
                    tmp.append(node.right.val)
            level = nextLevel
            if tmp: res.append(tmp)
        return res
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
        self.dfs(root, result, 0)
        result.reverse()
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

# Binary Tree Zigzag Level Order Traversal

> Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

> For example:

> Given binary tree [3,9,20,null,null,15,7],

> ```
    3
   / \
  9  20
    /  \
   15   7
```

> return its zigzag level order traversal as:

> ```
[
  [3],
  [20,9],
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
    def zigzagLevelOrder(self, root):
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
        if level % 2 == 0:
            result[level].append(root.val)
        else:
            result[level].insert(0, root.val)
        self.dfs(root.left, result, level + 1)
        self.dfs(root.right, result, level + 1)
```
