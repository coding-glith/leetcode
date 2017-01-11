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
        if not root: return False
        return self.pathSum(root, sum)
    
    def pathSum(self, root, target):
        if not root: return False  # this only happens at a node with one child
        if not root.left and not root.right: return target == root.val
        return self.pathSum(root.left, target - root.val) or self.pathSum(root.right, target - root.val)
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

The difference between the two solution is the first one modify sub at the time of calling the method, but the second solution change the sub first, so it needs to pop out the value once done with the path of current root.

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
        if not root: return []
        result = []
        self.getPath(result, [], root, sum)
        return result
    
    def getPath(self, result, sub, root, target):
        if not root: return
        if not root.left and not root.right:
            if target == root.val:
                result.append(list(sub+[root.val]))
        self.getPath(result, sub+[root.val], root.left, target-root.val)
        self.getPath(result, sub+[root.val], root.right, target-root.val)
```

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

# Path Sum III

> You are given a binary tree in which each node contains an integer value.

> Find the number of paths that sum to a given value.

> The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

> The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

> Example:

> ```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8
      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1
Return 3. The paths that sum to 8 are:
1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

Check explanation from leetcode [discussion](https://discuss.leetcode.com/topic/65100/2-python-solutions-with-detailed-explanation).

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
        :rtype: int
        """
        return self.getSum(root, sum, 0, {0:1})
    
    def getSum(self, root, target, cur, sumDict):
        if not root: return 0
        res, tmp = 0, cur + root.val - target
        if tmp in sumDict:
            res += sumDict[tmp]
        if cur + root.val not in sumDict:
            sumDict[cur+root.val] = 1
        else: sumDict[cur+root.val] += 1
        res += self.getSum(root.left, target, cur+root.val, sumDict)
        res += self.getSum(root.right, target, cur+root.val, sumDict)
        sumDict[cur+root.val] -= 1
        return res
```

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
        :rtype: int
        """
        if root:
            return self.getPath(root, sum) + \
                   self.pathSum(root.left, sum) + \
                   self.pathSum(root.right, sum)
        return 0
    
    def getPath(self, root, target):
        if root:
            return int(root.val == target) + \
                   self.getPath(root.left, target-root.val) + \
                   self.getPath(root.right, target-root.val)
        return 0
```

# Binary Tree Maximum Path Sum

> Given a binary tree, find the maximum path sum.

> For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path does not need to go through the root.

> For example:

> Given the below binary tree,

> ```
       1
      / \
     2   3
```

> Return 6.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    
    maxSum = float('-inf')
    
    def maxPathSum(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root == None:
            return
        self.pathSum(root)
        return self.maxSum
    
    def pathSum(self, root):
        if root == None:
            return 0
        leftSum = max(0, self.pathSum(root.left))
        rightSum = max(0, self.pathSum(root.right))
        self.maxSum = max(leftSum + rightSum + root.val, self.maxSum)
        return root.val + max(leftSum, rightSum)
```

