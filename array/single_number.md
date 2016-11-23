# Single Number

> Given an array of integers, every element appears twice except for one. Find that single one.

> Note:

> Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

```Python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 1:
            return nums[0]
        nums.sort()
        for i in xrange(0, len(nums)-1, 2):
            if nums[i] != nums[i+1]:
                return nums[i]
        return nums[-1]
```

# Single Number II

> Given an array of integers, every element appears three times except for one. Find that single one.

> Note:

> Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

```Python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) < 3: return nums[0]
        nums.sort()
        for i in xrange(0, len(nums)-2, 3):
            if nums[i] != nums[i+1] or nums[i] != nums[i+2]:
                return nums[i]
        return nums[-1]
```
