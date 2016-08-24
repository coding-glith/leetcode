# Sort Colors

> Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

> Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

> Note:

> You are not suppose to use the library's sort function for this problem.

> Follow up:

> A rather straight forward solution is a two-pass algorithm using counting sort.

> First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

> Could you come up with an one-pass algorithm using only constant space?

```Python
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        # sort the list by [0, zero), [zero, one), [one, two)
        zero, one = 0, 0
        for two in xrange(len(nums)):
            tmp = nums[two]
            nums[two] = 2
            if tmp < 2:  # if is 0 still needs this
                # because one >= zero
                nums[one] = 1
                one += 1
            if tmp == 0:
                nums[zero] = 0
                zero += 1
```
