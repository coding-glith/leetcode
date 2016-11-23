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

# Single Number III

> Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

> For example:

> Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

> Note:

> * The order of the result is not important. So in the above example, [5, 3] is also correct.

> * Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?

```Python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if len(nums) <= 2: return nums
        idx, res = 0, []
        nums.sort()
        while idx < len(nums) - 1:
            if nums[idx] != nums[idx+1]:
                res.append(nums[idx])
                idx += 1
            else:
                idx += 2
        if len(res) < 2: res.append(nums[-1])
        return res
```
