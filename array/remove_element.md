# Remove Element

> Given an array and a value, remove all instances of that value in place and return the new length.

> Do not allocate extra space for another array, you must do this in place with constant memory.

> The order of elements can be changed. It doesn't matter what you leave beyond the new length.

> Example:

> Given input array nums = [3,2,2,3], val = 3

> Your function should return length = 2, with the first two elements of nums being 2.

Since the order doesn't matter, so we can use two pointers to achieve O(logN) complexity, otherwise check one by one like move zeros, then it's O(N) complexity.

```Python
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        left, right = 0, len(nums)-1
        while left <= right:
            if nums[left] != val:
                left += 1
            else:
                if nums[right] != val:
                    nums[left] = nums[right]
                    right -= 1
                    left += 1
                else:
                    right -= 1
        return right+1
```
