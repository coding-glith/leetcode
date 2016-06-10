# Remove Duplicates from Sorted Array

> Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

> Do not allocate extra space for another array, you must do this in place with constant memory.

> For example,

> Given input array nums = [1,1,2],

> Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

```Python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 0:
            return 0
        newIndex, index = 0, 1
        while index < len(nums):
            if nums[index] != nums[newIndex]:
                nums[newIndex+1] = nums[index]
                index += 1
                newIndex += 1
            else:
                index += 1
        return newIndex + 1
```

# Remove Duplicates from Sorted Array II

> Follow up for "Remove Duplicates":

> What if duplicates are allowed at most twice?

> For example,

> Given sorted array nums = [1,1,1,2,2,3],

> Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.

```Python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) <= 1:
            return len(nums)
        newIndex, index = 1, 2
        while index < len(nums):
            if nums[index] == nums[newIndex] and nums[index] == nums[newIndex-1]:
                index += 1 
            else:
                nums[newIndex+1] = nums[index]
                index += 1
                newIndex += 1                   

        return newIndex + 1
```
