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
        pascalTri = []
        for row in xrange(numRows):
            rowList = []
            for index in xrange(row+1):
                if index == 0 or index == row:
                    rowList.insert(index, 1)
                else:
                    rowList.insert(index, pascalTri[row-1][index-1] + pascalTri[row-1][index])
            pascalTri.insert(row, rowList)

        return pascalTri
```

# Pascal's Triangle II

> Given an index k, return the kth row of the Pascal's triangle.

> For example, given k = 3,

> Return [1,3,3,1].

> Note:

> Could you optimize your algorithm to use only O(k) extra space?

Solution 1: in place modify return list. After initializing the list to be all 1s, updating the list for each row and always starts from end to the beginning.

```Python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        if rowIndex < 0:
            return []
        triRow = [1 for i in xrange(rowIndex+1)]
        for row in xrange(rowIndex+1):
            for index in xrange(row-1, 0, -1):
                triRow[index] = triRow[index] + triRow[index-1]
        return triRow
```

Solution 2: backtracking, call getRow() for each row. Time limit exceeded.

```Python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        if rowIndex < 0:
            return []
        triRow = []
        for index in xrange(rowIndex+1):
            if index == 0 or index == rowIndex:
                triRow.insert(index, 1)
            else:
                triRow.insert(index, self.getRow(rowIndex-1)[index-1] + self.getRow(rowIndex-1)[index])

        return triRow
```
