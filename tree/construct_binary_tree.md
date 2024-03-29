# Construct Binary Tree from Preorder and Inorder Traversal

> Given preorder and inorder traversal of a tree, construct the binary tree.

> Note: You may assume that duplicates do not exist in the tree.

For a given binary tree:

```
        1
      /   \
     2     3
    / \   / \
   4   5  6  7
```
pre-order traversal : [1, 2, 4, 5, 3, 6, 7]

in-order traversal  : [4, 2, 5, 1, 6, 3, 7]

post-order traversal: [4, 5, 2, 6, 7, 3, 1]

The key idea is to keep the index instead of passing a new array to do iteration. Otherwise it will exceed memory limit. To solve the problem, the idea is that pre-order traversal start from the root, if we find the root position in in-order, the left part is the left sub-tree of that root, and right part is the right sub-tree. Then we do the same for the subtree recursively.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        if preorder == []:
            return None
        inorderDict = {}  # help to quick locate
        for indx, val in enumerate(inorder):
            inorderDict[val] = indx
        return self.buildTreeRecursion(preorder, inorder, inorderDict, 0, 0, len(inorder)-1)
    
    def buildTreeRecursion(self, preorder, inorder, inorderDict, preStart, inStart, inEnd):
        if inStart > inEnd:
            return None
        root = TreeNode(preorder[preStart])
        root.left = self.buildTreeRecursion(preorder, inorder, inorderDict, preStart+1, inStart, inorderDict[preorder[preStart]]-1)
        root.right = self.buildTreeRecursion(preorder, inorder, inorderDict, preStart+inorderDict[preorder[preStart]]-inStart+1, inorderDict[preorder[preStart]]+1, inEnd)
        return root
```

# Construct Binary Tree from Inorder and Postorder Traversal

> Given inorder and postorder traversal of a tree, construct the binary tree.

> Note: You may assume that duplicates do not exist in the tree.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def buildTree(self, inorder, postorder):
        """
        :type inorder: List[int]
        :type postorder: List[int]
        :rtype: TreeNode
        """
        if postorder == []:
            return None
        inorderDict = {}
        for indx, val in enumerate(inorder):
            inorderDict[val] = indx
        return self.buildTreeRecursion(inorder, postorder, inorderDict, 0, len(inorder)-1, len(postorder)-1)
    
    def buildTreeRecursion(self, inorder, postorder, inorderDict, inStart, inEnd, postIndx):
        if inStart > inEnd:
            return None
        root = TreeNode(postorder[postIndx])
        root.left = self.buildTreeRecursion(inorder, postorder, inorderDict, inStart, inorderDict[postorder[postIndx]]-1, postIndx-(inEnd-inorderDict[postorder[postIndx]])-1)
        root.right = self.buildTreeRecursion(inorder, postorder, inorderDict, inorderDict[postorder[postIndx]]+1, inEnd, postIndx-1)
        return root
```
