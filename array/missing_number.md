# Missing Number

> Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

> For example,

> Given nums = [0, 1, 3] return 2.

> Note:

> Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

```Python
class Solution(object):
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return (len(nums)+1)*len(nums)/2 - sum(nums)
```

```Python
class Solution(object):
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums.sort()
        for i in xrange(len(nums)-1):
            if nums[i] + 1 != nums[i+1]: return nums[i] + 1
        return nums[-1] + 1 if nums[-1] < len(nums) else nums[0] - 1
```
