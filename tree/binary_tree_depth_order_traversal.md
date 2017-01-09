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
        if not root: return []
        result, stack = [], [root]
        while stack:
            node = stack.pop()
            result.append(node.val)
            if node.right: stack.append(node.right)
            if node.left: stack.append(node.left)
        return result
```

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

Recusive.

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
        if not root: return []
        return [root.val] + self.preorderTraversal(root.left) + self.preorderTraversal(root.right)
```

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
        if not root: return []
        res = []
        self.preTravs(res, root)
        return res
    
    def preTravs(self, res, root):
        if not root: return
        res.append(root.val)
        self.preTravs(res, root.left)
        self.preTravs(res, root.right)
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

This iterative solution is based on a stack. The key is the order to push values into the stack and how to play with next node.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def inorderTraversal(self, root):
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
                stack.append(tmpNode)
                tmpNode = tmpNode.left
            if stack != []:
                tmpNode = stack.pop()
                result.append(tmpNode.val)
                tmpNode = tmpNode.right
        return result
```
Recursive solution.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root: return []
        res = []
        self.inTravs(res, root)
        return res

    def inTravs(self, res, root):
        if not root: return
        self.inTravs(res, root.left)
        res.append(root.val)
        self.inTravs(res, root.right)
```

# Binary Tree Postorder Traversal

> Given a binary tree, return the postorder traversal of its nodes' values.

> For example:

> Given binary tree {1,#,2,3},

> ```
   1
    \
     2
    /
   3
```

> return [3,2,1].

> Note: Recursive solution is trivial, could you do it iteratively?

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root == None:
            return []
        result, stack = [], []
        tmpNode = root
        lastVisited = None
        while tmpNode or stack != []:
            while tmpNode:
                stack.append(tmpNode)
                tmpNode = tmpNode.left
            currentNode = stack[-1]
            if currentNode.right == None or currentNode.right == lastVisited:
                result.append(currentNode.val)
                stack.pop()       # only pop out after checked the value
                lastVisited = currentNode
                tmpNode = None    # make sure to check all node at the left tree first
            else:
                tmpNode = currentNode.right
        return result
```

Recursive solution

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root: return []
        res = []
        self.postTravs(res, root)
        return res
    
    def postTravs(self, res, root):
        if not root: return
        self.postTravs(res, root.left)
        self.postTravs(res, root.right)
        res.append(root.val)
```
