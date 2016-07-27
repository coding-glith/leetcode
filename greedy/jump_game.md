# Jump Game

> Given an array of non-negative integers, you are initially positioned at the first index of the array.

> Each element in the array represents your maximum jump length at that position.

> Determine if you are able to reach the last index.

> For example:

> A = [2,3,1,1,4], return true.

> A = [3,2,1,0,4], return false.

```Python

```

This DP solution is checking from end to start, but get 'time limit exceeded'. This is O(n^2) time complexity.

```Python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums) <= 1:
            return True
        result = [False for indx in xrange(len(nums))]
        result[len(nums)-1] = True
        for indx in xrange(len(nums)-2, -1, -1):
            for inner in xrange(indx+1, len(nums)):
                if nums[indx] >= (inner-indx) and result[inner] == True:
                    result[indx] = True
        return result[0]
```
