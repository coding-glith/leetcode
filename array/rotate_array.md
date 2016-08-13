# Rotate Array

> Rotate an array of n elements to the right by k steps.

> For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

> Note:

> Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

```Python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        if len(nums) == 0 or k == 0 or k % len(nums) == 0:
            return
        k %= len(nums)
        nums[:] = nums[-k:] + nums[:-k]
```

Intuitively, swap one by one, but this solution is O(n*k).

```Python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        if len(nums) == 0 or k == 0 or k % len(nums) == 0:
            return
        for r in xrange(k%len(nums)):
            tmp = nums[0]
            nums[0] = nums[len(nums)-1]
            for i in xrange(1, len(nums)):
                tmp1 = nums[i]
                nums[i] = tmp
                tmp = tmp1
        print nums
```
