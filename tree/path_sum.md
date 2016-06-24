# Path Sum

> Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

> For example:

> Given the below binary tree and sum = 22,

> ```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```

> return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        if root == None:
            return False
        return self.dfs(root, sum, 0)

    def dfs(self, root, target, pathSum):
        if root == None:
            return False
        pathSum += root.val
        if root.left == None and root.right == None:
            if pathSum == target:
                return True
            else:
                return False
        left = self.dfs(root.left, target, pathSum)
        right = self.dfs(root.right, target, pathSum)
        return left or right
```

# Path Sum II

> Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

> For example:

> Given the below binary tree and sum = 22,

> ```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

> return

> ```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

Don't understand why need to add list() statement when appending pathList to result.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: List[List[int]]
        """
        if root == None:
            return []
        result = []
        self.dfs(root, sum, 0, [], result)
        return result

    def dfs(self, root, target, pathSum, pathList, result):
        if root == None:
            return
        pathList.append(root.val)
        pathSum += root.val
        if root.left == None and root.right == None:
            if pathSum == target:
                result.append(list(pathList))  # need to state list() here, otherwise return [[]]
        else:
            self.dfs(root.left, target, pathSum, pathList, result)
            self.dfs(root.right, target, pathSum, pathList, result)
        pathList.pop()
```
