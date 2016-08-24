# Minimum Size Subarray Sum

> Given an array of n positive integers and a positive integer s, find the minimal length of a subarray of which the sum ≥ s. If there isn't one, return 0 instead.

> For example, given the array [2,3,1,2,4,3] and s = 7,

> the subarray [4,3] has the minimal length under the problem constraint.

> More practice:

> If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log n).

O(N) solution.

```Python
class Solution(object):
    def minSubArrayLen(self, s, nums):
        """
        :type s: int
        :type nums: List[int]
        :rtype: int
        """
        start, end, sumVal, minVal = 0, 0, 0, float('inf')
        while end < len(nums):
            # expand window until sumVal >= s
            while (sumVal < s and end < len(nums)):
                sumVal += nums[end]
                end += 1
            if sumVal >= s:
                # based on above method, shrink window must from left side
                while sumVal >= s and start < end:
                    sumVal -= nums[start]
                    start += 1
                    minVal = min(minVal, end + 1 - start)
        return minVal if minVal != float('inf') else 0
```
