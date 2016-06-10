# Pascal's Triangle

> Given numRows, generate the first numRows of Pascal's triangle.

> For example, given numRows = 5,

> Return

> ```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

```Python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        if numRows <= 0:
            return []
        pascalTri = [[1]]
        for row in xrange(1, numRows):
            rowList = []
            for index in xrange(row+1):
                if index == 0 or index == row:
                    rowList.insert(index, 1)
                else:
                    rowList.insert(index, pascalTri[row-1][index-1] + pascalTri[row-1][index])
            pascalTri.insert(row, rowList)

        return pascalTri
```
