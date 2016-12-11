# Search in Rotated Sorted Array

> Suppose a sorted array is rotated at some pivot unknown to you beforehand.

> (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

> You are given a target value to search. If found in the array return its index, otherwise return -1.

> You may assume no duplicate exists in the array.

First find out the pivot, then check which range the target lies, and finally do binary search.

```Python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if len(nums) == 1:
            return 0 if target in nums else -1
        # check if rotate
        piv = -1
        for i in xrange(len(nums)-1):
            if nums[i] > nums[i+1]:
                piv = i + 1
                break
        if piv == -1:
            start, end = 0, len(nums) - 1
        # if rotate, do binary search for that list
        else:
            if nums[-1] < target:
                start, end = 0, piv - 1
            else:
                start, end = piv, len(nums)-1
        while start <= end:
            mid = start + (end - start) / 2
            if nums[mid] < target:
                start = mid + 1
            elif nums[mid] > target:
                end = mid - 1
            else:
                return mid
        return -1
```

# Search in Rotated Sorted Array II

> Follow up for "Search in Rotated Sorted Array":

> What if duplicates are allowed?

> Would this affect the run-time complexity? How and why?

> Write a function to determine if a given target is in the array.

Yes, it would affect the time complexity. Above has O(logn) to find out the pivot, but below only has O(n) solution.

```Python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: bool
        """
        if len(nums) == 1:
            return target in nums
        # check if rotate
        piv = -1
        for i in xrange(len(nums)-1):
            if nums[i] > nums[i+1]:
                piv = i + 1
                break
        if piv == -1:
            start, end = 0, len(nums) - 1
        # if rotate, do binary search for that list
        else:
            if nums[-1] < target:
                start, end = 0, piv - 1
            else:
                start, end = piv, len(nums)-1
        while start <= end:
            mid = start + (end - start) / 2
            if nums[mid] < target:
                start = mid + 1
            elif nums[mid] > target:
                end = mid - 1
            else:
                return True
        return False
```
