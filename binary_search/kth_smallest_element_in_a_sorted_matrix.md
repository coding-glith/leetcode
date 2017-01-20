# Kth Smallest Element in a Sorted Matrix

> Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

> Note that it is the kth smallest element in the sorted order, not the kth distinct element.

> Example:

> ```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,
return 13.
```

> Note: 

> You may assume k is always valid, 1 ≤ k ≤ n^2.

Check leetcode [discussion](https://discuss.leetcode.com/topic/52948/share-my-thoughts-and-clean-java-code). This idea is to use binary search. There're other faster solutions. Please check.

```Python
class Solution(object):
    def kthSmallest(self, matrix, k):
        """
        :type matrix: List[List[int]]
        :type k: int
        :rtype: int
        """
        if not matrix or not matrix[0]: return None
        left, right = matrix[0][0], matrix[-1][-1]+1
        while left < right:
            mid = left + (right - left) / 2
            count = 0   # the number of values that's smaller than mid
            col = len(matrix[0]) - 1    # start count from larger to left
            for row in xrange(len(matrix)):
                while col >= 0 and matrix[row][col] > mid:
                    col -= 1
                count += col + 1    # matrix[row][:col+1] are smaller than mid
            if count < k: left = mid + 1
            else: right = mid
        return left
```
