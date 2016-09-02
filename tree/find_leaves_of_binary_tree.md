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

The idea is to use a dictionary to store the level and corresponding nodes' value.

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
        def levelDict(root, d):
            if not root:
                return 0
            left = levelDict(root.left, d)
            right = levelDict(root.right, d)
            level = max(left, right) + 1
            d[level] += [root.val]
            return level

        dic, res = collections.defaultdict(list), []
        levelDict(root, dic)
        for i in dic:
            res.append(dic[i])
        return res
```
