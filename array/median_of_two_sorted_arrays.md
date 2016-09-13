# Median of Two Sorted Arrays

> There are two sorted arrays nums1 and nums2 of size m and n respectively.

> Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

> Example 1:

> ```
nums1 = [1, 3]
nums2 = [2]
```

> The median is 2.0

> Example 2:

> ```
nums1 = [1, 2]
nums2 = [3, 4]
```

> The median is (2 + 3)/2 = 2.5

Good explanation from leetcode [discussion](https://discuss.leetcode.com/topic/4996/share-my-o-log-min-m-n-solution-with-explanation/2).

My method is quite easy to understand, but requires extra space. use pointers to check the two arrays and save the values into "smaller" and "larger" array. In this case, smaller and larger array are always the same size. The median is the value that divides the two arrays.

```Python
class Solution(object):
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        m, n = len(nums1), len(nums2)
        left1, right1, left2, right2 = 0, m-1, 0, n-1
        smaller, larger = [], []
        while left1 <= right1 and left2 <= right2:
            if nums1[left1] < nums2[left2]:
                smaller.append(nums1[left1])
                left1 += 1
            else:
                smaller.append(nums2[left2])
                left2 += 1
            if nums1[right1] > nums2[right2]:
                larger.append(nums1[right1])
                right1 -= 1
            else:
                larger.append(nums2[right2])
                right2 -= 1
        if left2 <= right2 or left1 <= right1:
            if left2 <= right2:
                left1, right1, nums1 = left2, right2, nums2
            if (right1 - left1) % 2 == 1:
                return (nums1[(left1+right1)/2] + nums1[(left1+right1)/2+1]) / 2.0
            else:
                return float(nums1[(left1+right1)/2])
        else:
            return (smaller[-1] + larger[-1]) / 2.0
```
