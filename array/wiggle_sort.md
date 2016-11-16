# Wiggle Sort

> Given an unsorted array nums, reorder it in-place such that nums[0] <= nums[1] >= nums[2] <= nums[3]....

> For example, given nums = [3, 5, 2, 1, 6, 4], one possible answer is [1, 6, 2, 5, 3, 4].

```Python
class Solution(object):
    def wiggleSort(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        for i in xrange(len(nums)-1):
            if (i % 2 == 0 and nums[i] > nums[i+1]) or (i % 2 == 1 and nums[i] < nums[i+1]):
                nums[i], nums[i+1] = nums[i+1], nums[i]
```

# Wiggle Sort II

> Given an unsorted array nums, reorder it such that nums[0] < nums[1] > nums[2] < nums[3]....

> Example:

> * Given nums = [1, 5, 1, 1, 6, 4], one possible answer is [1, 4, 1, 5, 1, 6]. 

> * Given nums = [1, 3, 2, 2, 3, 1], one possible answer is [2, 3, 1, 3, 1, 2].

> Note:

> You may assume all input has valid answer.

> Follow Up:

> Can you do it in O(n) time and/or in-place with O(1) extra space?

From leetcode [discussion](https://discuss.leetcode.com/topic/32861/3-lines-python-with-explanation-proof).

knowing the use of python list: array[start:end:step]

```Python
class Solution(object):
    def wiggleSort(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        nums.sort()
        half = len(nums[::2])-1
        nums[::2], nums[1::2] = nums[half::-1], nums[:half:-1]
```
