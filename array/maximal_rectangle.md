# Maximal Rectangle

> Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing all ones and return its area.

Based on [largest_rectangle_in_histogram](largest_rectangle_in_histogram.md), we can first create another matrix - heights, of which each value represents the height from this point to the top. But note if this point is '0', we set the height of this point to be 0, because heights represents value of consecutive '1's. Then go over each row again to find out the max rectangle.

```Python
class Solution(object):
    def maximalRectangle(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        # input value in the matrix is string
        if len(matrix) == 0:
            return 0
        heights = [[]]
        # each value in heights is the height from this point to top of this column
        for col in xrange(len(matrix[0])):
            if matrix[0][col] == '0':
                heights[0].append(0)
            else:
                heights[0].append(1)
        for row in xrange(1, len(matrix)):   # O(n*m)
            heights.append([])
            for col in xrange(len(matrix[row])):
                if matrix[row][col] == '0':
                    heights[row].append(0)
                else:
                    heights[row].append(heights[row-1][col] + 1)
        maxRect = 0
        print heights
        for row in xrange(len(matrix)):   # O(n*m)
            maxRect = max(maxRect, self.maxRectHist(heights[row]))
        return maxRect

    def maxRectHist(self, heights):
        if len(heights) == 0:
            return 0
        stack, maxArea, indx = [], 0, 0
        heights.append(0)
        while indx < len(heights):
            if stack == [] or heights[indx] > heights[stack[len(stack)-1]]:
                stack.append(indx)
                indx += 1
            else:
                top = stack[len(stack)-1]
                stack.pop()
                if stack == []:
                    maxArea = max(maxArea, heights[top] * indx)
                else:
                    maxArea = max(maxArea, heights[top] * (indx - stack[len(stack)-1] -1))
        return maxArea
```
