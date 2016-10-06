# Binary Tree Longest Consecutive Sequence

> Given a binary tree, find the length of the longest consecutive sequence path.

> The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

> For example,

> ```
   1
    \
     3
    / \
   2   4
        \
         5
```

> Longest consecutive sequence path is 3-4-5, so return 3.

> ```
   2
    \
     3
    / 
   2    
  / 
 1
```

> Longest consecutive sequence path is 2-3,not3-2-1, so return 2.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def longestConsecutive(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        res, stack = 0, [[root, 1]]  # cur node and length up to this node
        while stack:
            node, length = stack.pop()
            res = max(res, length)
            for child in [node.left, node.right]:
                if child:
                    l = length + 1 if child.val == node.val + 1 else 1
                    stack.append([child, l])
        return res
```

Recursive Solution.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def longestConsecutive(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root: return 0
        return max(self.getSeq(1, root.left, root.val), self.getSeq(1, root.right, root.val))

    def getSeq(self, count, root, val):
        if not root: return count
        if root.val - val == 1: count += 1
        else: count = 1
        left = self.getSeq(count, root.left, root.val)
        right = self.getSeq(count, root.right, root.val)
        return max(left, right, count)
```
