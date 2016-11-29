# Minimum Size Subarray Sum

> Given an array of n positive integers and a positive integer s, find the minimal length of a subarray of which the sum ≥ s. If there isn't one, return 0 instead.

> For example, given the array [2,3,1,2,4,3] and s = 7,

> the subarray [4,3] has the minimal length under the problem constraint.

> More practice:

> If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log n).

O(N) solution. Even though there's two loops, the two pointer start and i are like two runners, i runs faster and start runs slower, but they only go through the array once.

```Python
class Solution(object):
    def minSubArrayLen(self, s, nums):
        """
        :type s: int
        :type nums: List[int]
        :rtype: int
        """
        res, sumVal, flag, start = sys.maxint, 0, False, -1
        for i, val in enumerate(nums):
            sumVal += val
            if sumVal >= s:
                flag = True
                while sumVal >= s:
                    res = min(res, i - start)
                    start += 1
                    sumVal -= nums[start]
        return res if flag else 0
```
