# Sum Root to Leaf Numbers

> Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

> An example is the root-to-leaf path 1->2->3 which represents the number 123.

> Find the total sum of all root-to-leaf numbers.

> For example,

> ```
    1
   / \
  2   3
```

> The root-to-leaf path 1->2 represents the number 12.

> The root-to-leaf path 1->3 represents the number 13.

> Return the sum = 12 + 13 = 25.

Since the height of the subtree is different, so we cannot calculate the result along the path traverse. Here, we use a list to store every root to leaf sum value.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sumNumbers(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        result = []
        self.getSum(result, 0, root)
        return sum(result)
    
    def getSum(self, result, sumTill, root):
        if not root: return
        if not root.left and not root.right:
            result.append(sumTill*10 + root.val)
            return
        self.getSum(result, sumTill*10 + root.val, root.left)
        self.getSum(result, sumTill*10 + root.val, root.right)
```
