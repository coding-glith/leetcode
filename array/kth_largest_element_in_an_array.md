# Kth Largest Element in an Array

> Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

> For example,

> Given [3,2,1,5,6,4] and k = 2, return 5.

> Note: 

> You may assume k is always valid, 1 ≤ k ≤ array's length.

Implementation of quick sort algorightm.

```Python
class Solution(object):
    def quickSortImplementation(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        self.quickSort(nums, 0, len(nums)-1)
        return nums

    def quickSort(self, nums, low, high):
        if low >= high: return
        idx = self.partition(nums, low, high)
        self.quickSort(nums, low, idx-1)
        self.quickSort(nums, idx+1, high)

    def partition(self, nums, low, high):
        left, right = low + 1, high
        while left <= right:
            while nums[left] < nums[low] and left <= right:
                left += 1
            while nums[right] > nums[low] and left <= right:
                right -= 1
            if left >= right: break
            nums[left], nums[right] = nums[right], nums[left]
        nums[low], nums[right] = nums[right], nums[low]
        return right
```
