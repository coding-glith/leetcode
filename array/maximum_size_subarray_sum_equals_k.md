# Maximum Size Subarray Sum Equals k

> Given an array nums and a target value k, find the maximum length of a subarray that sums to k. If there isn't one, return 0 instead.

> Example 1:

> Given nums = [1, -1, 5, -2, 3], k = 3,

> return 4. (because the subarray [1, -1, 5, -2] sums to 3 and is the longest)

> Example 2:

> Given nums = [-2, -1, 2, 1], k = 1,

> return 2. (because the subarray [-1, 2] sums to 1 and is the longest)

> Follow Up:

> Can you do it in O(n) time?

nums:             [1, -1, 5, -2, 3]

accumulate sum:   [1,  0, 5,  3, 6]

sumDict: {0:-1, 1:0, 5:2, 3:3, 6:4}

The idea of this solution is to maintain a dictionary to keep track of the smallest index with the accumulate sum. And we only need to subtract the accumulate sum to get the target every time.

```Python
class Solution(object):
    def maxSubArrayLen(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        sumDict, res, sumVal = {0:-1}, 0, 0
        for i, val in enumerate(nums):
            sumVal += val   # sumVal is the accumulate sum from index 0
            if sumVal not in sumDict:  # only consider this case for longest subarray
                sumDict[sumVal] = i
            if sumVal - k in sumDict:
                res = max(res, i - sumDict[sumVal - k])
        return res
```
