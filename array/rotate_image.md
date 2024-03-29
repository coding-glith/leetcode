# Rotate Image

> You are given an n x n 2D matrix representing an image.

> Rotate the image by 90 degrees (clockwise).

> Follow up:

> Could you do this in-place?

```
always just check the left side.
1 2 | 3
4 5 | 6
7 8 | 9

1  2  | 3  4
5  6  | 7  8
9  10 | 11 12
13 14 | 15 16
```

```Python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        N = len(matrix)
        for row in xrange(N / 2):
            for col in xrange(N - N / 2): # for odd cases, need to use N-N/2 instead of N/2
                # array[~i] is the same as array[len-1-i]
                matrix[row][col], matrix[col][~row], matrix[~row][~col], matrix[~col][row] = \
                matrix[~col][row], matrix[row][col], matrix[col][~row], matrix[~row][~col]
```
