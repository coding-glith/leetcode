# Product of Array Except Self

> Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

> Solve it without division and in O(n).

> For example, given [1,2,3,4], return [24,12,8,6].

> Follow up:

> Could you solve it with constant space complexity? (Note: The output array does not count as extra space for the purpose of space complexity analysis.)

Without O(1) extra space.

```Python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        res = [1] * len(nums)
        for i in xrange(1, len(nums)):
            res[i] = nums[i-1] * res[i-1]
        prev = 1
        for i in xrange(len(nums)-2, -1, -1):
            res[i] *= nums[i+1] * prev
            prev *= nums[i+1]
        return res
```

```Python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if not nums:
            return nums
        res = [1]
        # get the product before current value
        for i in xrange(1, len(nums)):
            res.append(res[i-1] * nums[i-1])
        tmp = [1]
        # get the product after current value
        for i in xrange(1, len(nums)):
            tmp.append(tmp[i-1] * nums[len(nums)-i])
        for i in xrange(len(res)):
            res[i] *= tmp[len(res)-1-i]
        return res
```
