# First Missing Positive

> Given an unsorted integer array, find the first missing positive integer.

> For example,

> * Given [1,2,0] return 3,

> * and [3,4,-1,1] return 2.

> Your algorithm should run in O(n) time and uses constant space.

```Python
class Solution(object):
    def firstMissingPositive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums: return 1
        nums.sort()
        start = 0 if nums[0] > 0 else None
        for i in xrange(len(nums)):
            if nums[i] <= 0: start = i + 1
            break
        if start == None: return 1
        count = 1
        for j in xrange(start, len(nums)):
            if nums[j] > count: return count
            elif nums[j] == count: count += 1
        return count
```
