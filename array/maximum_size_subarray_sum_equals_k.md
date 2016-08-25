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

This solution is really tricky, need to construct the sumDict. :-(

```Python
class Solution(object):
    def maxSubArrayLen(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        sumDict, res, sumVal = {0:0}, 0, 0
        for i in xrange(len(nums)):
            sumVal += nums[i]
            wanted = sumVal - k
            if wanted in sumDict:
                length = i + 1 - sumDict[wanted]
                if res == 0 or length > res:
                    res = length
            if sumVal not in sumDict:
                sumDict[sumVal] = i + 1
        return res or 0
```
