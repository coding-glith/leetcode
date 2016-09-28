# Maximum Depth of Binary Tree

> Given a binary tree, find its maximum depth.

> The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

DFS, recursice, visit leaves first.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root is None:
            return 0
        leftDepth = self.maxDepth(root.left)
        rightDepth = self.maxDepth(root.right)

        return max(leftDepth, rightDepth) + 1
```

BFS, level order traversal

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        res = 0
        level = [root] if root else []
        while level:
            res += 1
            nextLevel = []
            for node in level:
                if node.left:
                    nextLevel.append(node.left)
                if node.right:
                    nextLevel.append(node.right)
            level = nextLevel
        return res
```

# Minimum Depth of Binary Tree

> Given a binary tree, find its minimum depth.

> The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        if not root.left or not root.right:
            return self.minDepth(root.left) + self.minDepth(root.right) + 1
        return min(self.minDepth(root.left), self.minDepth(root.right)) + 1
```

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        return self.helper(root)
        
        
    def helper(self, root):
        if not root:   # in case root only have one child
            return sys.maxint
        if not root.left and not root.right:   # for a leaf node
            return 1
        return min(self.helper(root.left), self.helper(root.right)) + 1
```

Iterative solution. BFS.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        depth, level = 0, [root]
        while root:
            nextLevel = []
            for node in level:
                if not node.left and not node.right:   # meet the first leaf, return
                    return depth + 1
                if node.left:
                    nextLevel.append(node.left)
                if node.right:
                    nextLevel.append(node.right)
            level = nextLevel
            depth += 1
        return depth
```
