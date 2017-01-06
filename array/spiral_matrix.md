# Spiral Matrix

> Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

> For example,

> Given the following matrix:

> ```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```

> You should return [1,2,3,6,9,8,7,4,5].

```Python
class Solution(object):
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        # the interesting part is matrix gets truncated every round
        res = []
        while matrix:
            # left to right
            res.extend(matrix.pop(0))  # extend list by appending elements from the iterable; append object the end
            # top down
            if matrix and matrix[0]:
                for row in matrix:
                    res.append(row.pop())
            # right to left
            if matrix:
                res.extend(matrix.pop()[::-1])  # [::-1] is to reverse array
            # bottom up
            if matrix and matrix[0]:
                for row in matrix[::-1]:
                    res.append(row.pop(0))
        return res
```

```Python
class Solution(object):
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        if not matrix or not matrix[0]: return []
        result = []
        self.spiral(result, matrix, 0, len(matrix)-1, 0, len(matrix[0])-1)
        return result
    
    def spiral(self, result, matrix, startRow, endRow, startCol, endCol):
        if startRow > endRow or startCol > endCol: return
        result += matrix[startRow][startCol:endCol+1]
        for i in xrange(startRow+1, endRow+1):
            result += [matrix[i][endCol]]
        if startRow != endRow: result += matrix[endRow][startCol:endCol][::-1]
        if startCol != endCol:
            for j in xrange(endRow-1, startRow, -1):
                result += [matrix[j][startCol]]
        self.spiral(result, matrix, startRow + 1, endRow - 1, startCol + 1, endCol - 1)
```

# Spiral Matrix II

> Given an integer n, generate a square matrix filled with elements from 1 to n^2 in spiral order.

> For example,

> Given n = 3,

> You should return the following matrix:

> ```
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

This solution needs to understand matrix index extremely well. di, dj do the spiral job.

```Python
class Solution(object):
    def generateMatrix(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        res = [[0] * n for _ in xrange(n)]
        row, col, di, dj = 0, 0, 0, 1
        for i in xrange(1, n*n+1):
            res[row][col] = i
            if res[(row+di)%n][(col+dj)%n]:
                di, dj = dj, -di
            row += di
            col += dj
        return res
```

```Python
class Solution(object):
    def generateMatrix(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        result = [[0] * n for _ in xrange(n)]
        self.spiral(result, 1, 0, n-1, 0, n-1)
        return result
    
    def spiral(self, result, startVal, startRow, endRow, startCol, endCol):
        if startRow > endRow or startCol > endCol: return
        for i in xrange(startCol, endCol+1):
            result[startRow][i] = startVal
            startVal += 1
        for i in xrange(startRow+1, endRow+1):
            result[i][endCol] = startVal
            startVal += 1
        if startRow != endRow:
            for i in xrange(endCol-1, startCol-1, -1):
                result[endRow][i] = startVal
                startVal += 1
        if startCol != endCol:
            for i in xrange(endRow-1, startRow, -1):
                result[i][startCol] = startVal
                startVal += 1
        self.spiral(result, startVal, startRow + 1, endRow - 1, startCol + 1, endCol - 1)
```
