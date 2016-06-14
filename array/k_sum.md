# Two Sum

> Given an array of integers, return indices of the two numbers such that they add up to a specific target.

> You may assume that each input would have exactly one solution.

> Example:

> ```
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

```Python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        dict = {}
        for indx in xrange(len(nums)):
            if dict.has_key(target - nums[indx]):
                return [dict[target - nums[indx]], indx]
            else:
                dict[nums[indx]] = indx
        return []
```
