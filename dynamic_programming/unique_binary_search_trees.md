# Unique Binary Search Trees

> Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

> For example,

> Given n = 3, there are a total of 5 unique BST's.

> ```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

The idea here is for 1 <= indx <= n, the number of BST is BSTnum(0, indx-1) * BSTnum(indx+1, n)

```Python
class Solution(object):
    def numTrees(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n <= 1:
            return 1
        BSTnum = [0 for indx in range(n+1)]
        BSTnum[0] = 1
        BSTnum[1] = 1
        for indx in range(2, n+1):
            for left in range(indx):
                BSTnum[indx] += BSTnum[left] * BSTnum[indx-left-1]
        return BSTnum[n]
```

# Unique Binary Search Trees II

> Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.

> For example,

> Given n = 3, your program should return all 5 unique BST's shown below.

> ```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

```Python

```
