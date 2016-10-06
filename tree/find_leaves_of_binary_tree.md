# Find Leaves of Binary Tree

> Given a binary tree, collect a tree's nodes as if you were doing this: Collect and remove all leaves, repeat until the tree is empty.

> Example:

> Given binary tree 

> ```
          1
         / \
        2   3
       / \     
      4   5    
```

> Returns [4, 5, 3], [2], [1].

> Explanation:

> * Removing the leaves [4, 5, 3] would result in this tree:

> ```
          1
         / 
        2          
```

> * Now removing the leaf [2] would result in this tree:

> ```
          1          
```

> * Now removing the leaf [1] would result in the empty tree:

> ```
          []         
```

> Returns [4, 5, 3], [2], [1].

Bottom up solution, calculate level from leaf to parent.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def findLeaves(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root: return []
        res = []
        self.getLeaves(res, root)
        return res

    def getLeaves(self, res, root):
        if not root: return 0
        leftLevel = self.getLeaves(res, root.left)
        rightLevel = self.getLeaves(res, root.right)
        level = max(leftLevel, rightLevel) + 1
        if len(res) <= level - 1:
            res.append([])
        res[level-1].append(root.val)
        return level
```
