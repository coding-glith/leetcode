# Find Peak Element

> A peak element is an element that is greater than its neighbors.

> Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.

> The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

> You may imagine that num[-1] = num[n] = -∞.

> For example, in array [1, 2, 3, 1], 3 is a peak element and your function should return the index number 2.

> Note:

> Your solution should be in logarithmic complexity.

The reason this question can be solved by binary search is because for a random number cur, we can choose to go either side to find the peak, for example, if cur < cur + 1 and we go right, there must be a peak, otherwise cur + 1 < cur + 2 < ... < n-1 < n (n's the peak), if n-1 > n, then n-1's the peak.

```Python
class Solution(object):
    def findPeakElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 0:
            return
        if len(nums) == 1:
            return 0
        
        start, end = 0, len(nums)-1
        while start <= end:
            midIndex = start + (end - start) / 2
            if midIndex == 0:
                return midIndex if nums[midIndex] > nums[midIndex+1] else midIndex + 1
            elif midIndex == len(nums)-1:
                return midIndex if nums[midIndex] > nums[midIndex-1] else midIndex - 1
            else:
                if nums[midIndex] > nums[midIndex-1] and nums[midIndex] > nums[midIndex+1]:
                    return midIndex
                elif nums[midIndex] < nums[midIndex-1]:
                    end = midIndex - 1
                else:
                    start = midIndex + 1
```
