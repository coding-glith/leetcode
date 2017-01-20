# Kth Largest Element in an Array

> Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

> For example,

> Given [3,2,1,5,6,4] and k = 2, return 5.

> Note: 

> You may assume k is always valid, 1 ≤ k ≤ array's length.

Quick selection. based on quicksort algorithm, everytime the partition part will put the nums[low] at the position "right", so the kth largest is the len(nums)-k at nums' index. We just need to check if the returned index is the one we want, otherwise keeps tracking either the left or the right side.

```Python
class Solution(object):
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        if k <= 0 or k > len(nums): return None
        left, right = 0, len(nums) - 1
        while left < right:
            idx = self.partition(nums, left, right)
            if idx == len(nums) - k: return nums[idx]
            elif idx < len(nums) - k:
                left = idx + 1
            else:
                right = idx - 1
        return nums[len(nums) - k]
    
    def partition(self, nums, low, high):
        if low >= high: return
        left, right = low + 1, high
        while left <= right:
            while left <= right and nums[left] < nums[low]:
                left += 1
            while left <= right and nums[right] >= nums[low]:
                right -= 1
            if left >= right: break
            nums[left], nums[right] = nums[right], nums[left]
        nums[low], nums[right] = nums[right], nums[low]
        return right
```

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
            while left <= right and nums[left] < nums[low]:
                left += 1
            while left <= right and nums[right] >= nums[low]:
                right -= 1
            if left >= right: break
            nums[left], nums[right] = nums[right], nums[left]
        nums[low], nums[right] = nums[right], nums[low]
        return right
```
