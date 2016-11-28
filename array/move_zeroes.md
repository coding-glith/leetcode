# Move Zeroes

> Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

> For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

> Note:

> * You must do this in-place without making a copy of the array.

> * Minimize the total number of operations.

O(N) time complexity and O(N) operations.

```Python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        nonZero = -1
        for i, val in enumerate(nums):
            if val == 0: nonZero = i; break
        if nonZero == -1: return
        for i in xrange(len(nums)):
            if nums[i] != 0 and i > nonZero:
                nums[nonZero], nums[i] = nums[i], 0
                nonZero += 1
```

```Python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        if len(nums) == 0:
            return
        for i in xrange(len(nums)):
            if nums[i] == 0:
                for inner in xrange(i+1, len(nums)):
                    if nums[inner] != 0:
                        nums[i], nums[inner] = nums[inner], nums[i]
                        break
```
