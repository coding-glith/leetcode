# Merge Sorted Array

> Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

> Note:

> You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

Updating from m+n-1 with comparison of two list. Not sure why when m == 0, cannot assign nums1 = nums2. Leetcode only allow nums1[0:n] = nums2[0:n] to pass.

```Python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        if m == 0:
            nums1[0:n] = nums2[0:n]
            return
        if n == 0:
            return
        nums1Ind, nums2Ind = m-1, n-1
        for index in xrange(m+n-1, -1, -1):
            if nums1[nums1Ind] < nums2[nums2Ind]:
                nums1[index] = nums2[nums2Ind]
                nums2Ind -= 1
            else:
                nums1[index] = nums1[nums1Ind]
                nums1Ind -= 1
            if nums1Ind == -1:
                nums1[0:nums2Ind+1] = nums2[0:nums2Ind+1]
                break
            if  nums2Ind == -1:
                break
```
