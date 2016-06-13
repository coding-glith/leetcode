# Find Minimum in Rotated Sorted Array

> Suppose a sorted array is rotated at some pivot unknown to you beforehand.

> (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

> Find the minimum element.

> You may assume no duplicate exists in the array.

```Python
class Solution(object):
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        result = 0
        for index in xrange(1, len(nums)):
            if nums[index] < nums[result]:
                result = index
                break
        
        return nums[result]
```

# Find Minimum in Rotated Sorted Array II

> Follow up for "Find Minimum in Rotated Sorted Array":

> What if duplicates are allowed?

> Would this affect the run-time complexity? How and why?

> Suppose a sorted array is rotated at some pivot unknown to you beforehand.

> (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

> Find the minimum element.

> The array may contain duplicates.

```Python
class Solution(object):
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        resIndex = 0
        for index in xrange(1, len(nums)):
            if nums[index] < nums[resIndex]:
                resIndex = index
                break
        
        return nums[resIndex]
```
