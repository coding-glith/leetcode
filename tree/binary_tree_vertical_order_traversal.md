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

Derived from level order traversal, the difference here is to maintain a level marker of which vertical level the current node is. Say root has level 0, it's left child is -1 and right child 1, and so on. Then sort the level and append to the result.

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
        if not root: return []
        res, queue, levelDict = [], [[root, 0]], {}
        while queue:
            node, vertLevel = queue.pop(0)
            levelDict[vertLevel] = levelDict.get(vertLevel, []) + [node.val]
            if node.left:
                queue.append([node.left, vertLevel - 1])
            if node.right:
                queue.append([node.right, vertLevel + 1])
        for key in sorted(levelDict.keys()):
            res.append(levelDict[key])
        return res
```
