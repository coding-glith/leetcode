# Majority Element

> Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

> You may assume that the array is non-empty and the majority element always exist in the array.

Python has a method "count()" for array to count the frequency of an element. But here we go through the array and count one by one.

```Python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        numDict = {}
        for i in xrange(len(nums)):
            if nums[i] not in numDict:
                numDict[nums[i]] = 0
            else:
                numDict[nums[i]] += 1
            if numDict[nums[i]] >= len(nums) / 2:
                return nums[i]
```

# Majority Element II

> Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times. The algorithm should run in linear time and in O(1) space.

```Python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        nums.sort()
        nums.append(float('inf'))
        res, start = [], 0
        for i in xrange(len(nums)-1):
            if nums[i] != nums[i+1]:
                if (i+1-start) > (len(nums)-1)/3:
                    res.append(nums[i])
                start = i + 1
        return res
```
