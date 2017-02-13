# Find Largest Value in Each Tree Row

> You need to find the largest value in each row of a binary tree.

> Example:

> ```
Input: 
          1
         / \
        3   2
       / \   \  
      5   3   9 
Output: [1, 3, 9]
```

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def largestValues(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root: return []
        result = [root.val]
        level = [root]
        while level:
            nextLevel, maxVal = [], -sys.maxint-1
            for node in level:
                if node.left:
                    maxVal = max(maxVal, node.left.val)
                    nextLevel.append(node.left)
                if node.right:
                    maxVal = max(maxVal, node.right.val)
                    nextLevel.append(node.right)
            level = nextLevel
            if level: result.append(maxVal)
        return result
```
