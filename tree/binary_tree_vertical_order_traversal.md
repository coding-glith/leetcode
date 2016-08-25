# Binary Tree Vertical Order Traversal

> Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).

> If two nodes are in the same row and column, the order should be from left to right.

> Examples:

> Given binary tree [3,9,20,null,null,15,7],

> ```
   3
  /\
 /  \
 9  20
    /\
   /  \
  15   7
```

> return its vertical order traversal as:

> ```
[
  [9],
  [3,15],
  [20],
  [7]
]
```

> Given binary tree [3,9,8,4,0,1,7],

> ```
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
```

> return its vertical order traversal as:

> ```
[
  [4],
  [9],
  [3,0,1],
  [8],
  [7]
]
```

> Given binary tree [3,9,8,4,0,1,7,null,null,null,2,5], (0's right child is 2 and 1's left child is 5),

> ```
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
    /\
   /  \
   5   2
```

> return its vertical order traversal as:

> ```
[
  [4],
  [9,5],
  [3,0,1],
  [8,2],
  [7]
]
```

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def verticalOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root:
            return []
        q, node, output = [], root, {}
        q.append([node, 0])
        while len(q) > 0:
            node, level = q.pop(0)   # pop the first item
            if level not in output:
                output[level] = [node.val]
            else:
                output[level].append(node.val)

            if node.left:
                q.append([node.left, level - 1])
            if node.right:
                q.append([node.right, level + 1])
        res = []
        for i in sorted(output.keys()):
            res.append(output[i])
        return res
```
