# Triangle

> Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

> For example, given the following triangle

> ```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

> The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

> Note:

> Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

At first, my intuition is to calculate the minSum by finding the neighboring minimum value of each row. This idea is not correct because for [[-1],[2,3],[1,-1,-3]], the answer should be -1->3->-3 instead of -1->2->-1.

What if we maintain the state of each value at the bottom row and trace up?

```Python
class Solution(object):
    def minimumTotal(self, triangle):
        """
        :type triangle: List[List[int]]
        :rtype: int
        """
        if len(triangle) == 0:
            return 0
        rowNum = len(triangle)
        # minSum[indx] represents minimum sum along the bottom value
        minSum = []
        for indx in range(len(triangle[rowNum-1])):
            minSum.append(triangle[rowNum-1][indx])
        for row in range(rowNum-2, -1, -1):
            for indx in range(row+1):
                minSum[indx] = min(minSum[indx], minSum[indx+1]) + triangle[row][indx]
        return minSum[0]
```
