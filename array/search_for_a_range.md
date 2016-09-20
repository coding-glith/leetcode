# Search for a Range

> Given a sorted array of integers, find the starting and ending position of a given target value.

> Your algorithm's runtime complexity must be in the order of O(log n).

> If the target is not found in the array, return [-1, -1].

> For example,

> Given [5, 7, 7, 8, 8, 10] and target value 8,

> return [3, 4].

```Python
class Solution(object):
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        res, left, right = [], 0, len(nums)-1
        while left <= right:
            mid = left + (right - left) / 2
            if nums[mid] >= target:
                right = mid - 1
            else:
                left = mid + 1
        if left < len(nums) and nums[left] == target:
            res.append(left)
        left, right = 0, len(nums)-1
        while left <= right:
            mid = left + (right - left) / 2
            if nums[mid] <= target:
                left = mid + 1
            else:
                right = mid - 1
        if right > 0 and nums[right] == target:
            res.append(right)
        if not res:
            return [-1, -1]
        elif len(res) == 1:
            return [res[0], res[0]]
        else:
            return res
```

```Python
class Solution(object):
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        result = [-1, -1]
        for index in xrange(len(nums)):
            if nums[index] == target:
                if result[0] == -1:
                    result[0] = index
                else:
                    result[1] = index
        if result[1] < result[0]:
            result[1] = result[0]

        return result
```
