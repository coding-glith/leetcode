# Verify Preorder Sequence in Binary Search Tree

> Given an array of numbers, verify whether it is the correct preorder traversal sequence of a binary search tree.

> You may assume each number in the sequence is unique.

> Follow up:

> Could you do it using only constant space complexity?

O(1) space complexity.

```Python
class Solution(object):
    def verifyPreorder(self, preorder):
        """
        :type preorder: List[int]
        :rtype: bool
        """
        lower = -1 << 31
        i = 0
        for x in preorder:
            if x < lower:
                return False
            while i > 0 and x > preorder[i-1]:
                lower = preorder[i-1]
                i -= 1
            preorder[i] = x
            i += 1
        return True
```

Use stack.

```Python
class Solution(object):
    def verifyPreorder(self, preorder):
        """
        :type preorder: List[int]
        :rtype: bool
        """
        stack = []
        lower = -1 << 31
        for x in preorder:
            if x < lower:
                return False
            while stack and x > stack[-1]:
                lower = stack.pop()
            stack.append(x)
        return True
```

My recursive solution exceeds time limit.

```Python
class Solution(object):
    def verifyPreorder(self, preorder):
        """
        :type preorder: List[int]
        :rtype: bool
        """
        if len(preorder) <= 1:
            return True
        root, piv = preorder[0], -1
        for i in xrange(1, len(preorder)):
            if preorder[i] > root:
                piv = i
                break
        if piv != -1:
            for j in xrange(piv, len(preorder)):
                if preorder[j] <= root:
                    return False
            return self.verifyPreorder(preorder[1:piv]) and self.verifyPreorder(preorder[piv:])
        else:
            return self.verifyPreorder(preorder[1:])
```
