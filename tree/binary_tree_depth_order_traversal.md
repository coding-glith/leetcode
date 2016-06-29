# Binary Tree Preorder Traversal

> Given a binary tree, return the preorder traversal of its nodes' values.

> For example:

> Given binary tree {1,#,2,3},

> ```
   1
    \
     2
    /
   3
```

> return [1,2,3].

> Note: Recursive solution is trivial, could you do it iteratively?

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root == None:
            return []
        result, stack = [], []
        tmpNode = root
        while tmpNode or stack != []:
            while tmpNode:
                result.append(tmpNode.val)
                stack.append(tmpNode)
                tmpNode = tmpNode.left
            if stack != []:
                tmpNode = stack.pop()
                tmpNode = tmpNode.right
        return result
```

# Binary Tree Inorder Traversal

> Given a binary tree, return the inorder traversal of its nodes' values.

> For example:

> Given binary tree [1,null,2,3],

> ```
   1
    \
     2
    /
   3
```

> return [1,3,2].

> Note: Recursive solution is trivial, could you do it iteratively?

```Python

```
