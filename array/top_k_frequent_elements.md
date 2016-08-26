# Top K Frequent Elements

> Given a non-empty array of integers, return the k most frequent elements.

> For example,

> Given [1,1,1,2,2,3] and k = 2, return [1,2].

> Note: 

> * You may assume k is always valid, 1 ≤ k ≤ number of unique elements.

> * Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

```Python
class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        if not nums:
            return nums
        nums.sort()
        ref, val, freq = [], nums[0], 1
        for i in xrange(1, len(nums)):
            if nums[i] == val:
                freq += 1
            else:
                ref.append([freq, val])
                freq, val = 1, nums[i]
        ref.append([freq, val])
        ref.sort()
        res = []
        for i in xrange(k):
            res.append(ref[len(ref)-1-i][1])
        return res
```
