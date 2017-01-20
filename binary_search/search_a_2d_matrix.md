# Search a 2D Matrix

> Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

> * Integers in each row are sorted from left to right.

> * The first integer of each row is greater than the last integer of the previous row.

> For example,

> Consider the following matrix:

> ```
[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
```

> Given target = 3, return true.

First, do binary search to find the row, then do binary search for that row.

```Python
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if not matrix or not matrix[0]: return False
        left, right = 0, len(matrix)-1
        while left < right-1:
            mid = left + (right - left) / 2
            if matrix[mid][0] == target: return True
            elif matrix[mid][0] < target:
                left = mid
            else:
                right = mid
        if matrix[right][0] <= target:
            left = right
        small, large = 0, len(matrix[left])-1
        while small <= large:
            mid = small + (large - small) / 2
            if matrix[left][mid] == target: return True
            elif matrix[left][mid] > target: large = mid - 1
            else: small = mid + 1
        return False
```

```Python
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if not matrix or len(matrix[0]) == 0:
            return False
        # first find the row
        left, right = 0, len(matrix)-1
        while left <= right:
            mid = left + (right - left) / 2
            if matrix[mid][0] == target:
                return True
            elif matrix[mid][0] > target:
                right = mid - 1
            else:
                if mid == len(matrix) - 1:
                    left = mid
                    break
                else:
                    if matrix[mid+1][0] == target:
                        return True
                    elif matrix[mid+1][0] > target:
                        left = mid
                        break
                    else:
                        left = mid + 1
        # do binary search
        start, end = 0, len(matrix[left]) - 1
        while start <= end:
            mid = start + (end - start) / 2
            if matrix[left][mid] == target:
                return True
            elif matrix[left][mid] > target:
                end = mid - 1
            else:
                start = mid + 1
        return False
```

```Python
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if len(matrix) == 0:
            return False
        index = 0
        while index < len(matrix):
            if target >= matrix[index][0] and target <= matrix[index][len(matrix[index])-1]:
                start, end = 0, len(matrix[index]) - 1   # binary search
                while start <= end:
                    mid = start + (end - start) / 2
                    if target == matrix[index][mid]:
                        return True
                    elif target < matrix[index][mid]:
                        end = mid - 1
                    else:
                        start = mid + 1
                if start > end:
                    return False
                index += 1
            elif target < matrix[index][0]:
                return False
            else:
                index += 1
        if index == len(matrix):
            return False
```

# Search a 2D Matrix II

> Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

> * Integers in each row are sorted in ascending from left to right.

> * Integers in each column are sorted in ascending from top to bottom.

> For example,

> Consider the following matrix:

> ```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

> Given target = 5, return true.

> Given target = 20, return false.

The key of this solution is to start from the left-bottom.

```Python
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if len(matrix) == 0:
            return False
        row, col = len(matrix) - 1, 0
        while row >= 0 and col < len(matrix[row]):
            if matrix[row][col] == target:
                return True
            elif matrix[row][col] > target:
                row -= 1
            else:
                col += 1
        return False
```
