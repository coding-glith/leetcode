# Search Insert Position

> Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

> You may assume no duplicates in the array.

> Here are few examples.

> [1,3,5,6], 5 → 2

> [1,3,5,6], 2 → 1

> [1,3,5,6], 7 → 4

> [1,3,5,6], 0 → 0

```Python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = left + (right - left) / 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid - 1
                if right < left:
                    return right + 1
            else:
                left = mid + 1
                if left > right:
                    return left
```

```Python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        for index in xrange(len(nums)):
            if nums[index] >= target:
                result = index
                break
            else:
                result = index + 1
        return result
```

# Longest Increasing Subsequence

> Given an unsorted array of integers, find the length of longest increasing subsequence.

> For example,

> Given [10, 9, 2, 5, 3, 7, 101, 18],

> The longest increasing subsequence is [2, 3, 7, 101], therefore the length is 4. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

> Your algorithm should run in O(n2) complexity.

> Follow up: Could you improve it to O(n log n) time complexity?

```Python
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        longest = [0] * len(nums)
        longest[0], idx = nums[0], 0   # idx is the index for the last elem in longest
        for i in xrange(1, len(nums)):
            # use binary search to find the position, such that:
            # longest[pos-1] < nums[i] and nums[i] < longest[pos]
            pos = self.binarySearch(longest, idx, nums[i])
            if nums[i] < longest[pos]:
                longest[pos] = nums[i]  # replace
            if pos > idx:
                idx, longest[idx] = pos, nums[i]  # append larger value
        return idx + 1

    def binarySearch(self, longest, idx, val):
        '''this function return the position where val should be inserted'''
        # longest always append largest value, so dp is sorted
        left, right = 0, idx
        while left <= right:
            mid = left + (right - left) / 2
            if longest[mid] == val:
                return mid
            elif longest[mid] < val:
                left = mid + 1
                if left > right: return left
            else:
                right = mid - 1
                if right < left: return right + 1
```
