# Set Matrix Zeroes

> Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

> Follow up:

> Did you use extra space?

> A straight forward solution using O(mn) space is probably a bad idea.

> A simple improvement uses O(m + n) space, but still not the best solution.

> Could you devise a constant space solution?

The trick of this in-place solution is to set to be other distinguished characters then set back to zeros. Can also be done by bit manipulation, like [Game of Life](game_of_life.md).

```Python
class Solution(object):
    def setZeroes(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        for row in xrange(len(matrix)):
            for col in xrange(len(matrix[0])):
                if matrix[row][col] == 0:
                    for thisCol in xrange(len(matrix[0])):
                        if matrix[row][thisCol] != 0:
                            matrix[row][thisCol] = '*'
                    for thisRow in xrange(len(matrix)):
                        if matrix[thisRow][col] != 0:
                            matrix[thisRow][col] = '*'
        for row in xrange(len(matrix)):
            for col in xrange(len(matrix[0])):
                if matrix[row][col] == '*':
                    matrix[row][col] = 0
```
