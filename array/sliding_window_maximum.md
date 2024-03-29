# Sliding Window Maximum

> Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

> For example,

> Given nums = [1,3,-1,-3,5,3,6,7], and k = 3.

> ```
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
Therefore, return the max sliding window as [3,3,5,5,6,7].
```

> Note: 

> * You may assume k is always valid, ie: 1 ≤ k ≤ input array's size for non-empty array.

> Follow up:

> * Could you solve it in linear time?

> Hint:

> * How about using a data structure such as deque (double-ended queue)?

> * The queue size need not be the same as the window’s size.

> * Remove redundant elements and the queue should store only elements that need to be considered.

The idea of this solution is to maintain a queue, in which the first element always is the index for the largest value, therefore the queue is in decending order. And in order to maintain the window size, every time it's out of window size, need to pop out the very left value in queue.

```Python
class Solution(object):
    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        res, queue = [], collections.deque()
        for i, val in enumerate(nums):
            while queue and nums[queue[-1]] < val:
                queue.pop()   # make sure queue is in decreasing order
            queue.append(i)
            if queue[0] == i - k:
                queue.popleft()   # out of window size
            if i >= k - 1:   # full window, get value
                res.append(nums[queue[0]])
        return res
```
