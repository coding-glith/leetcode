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
        left, right = 0, len(nums)
        while left < right:
            mid = left + (right - left) / 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid  # mid - 1 might be smaller, so check with mid again
            else:
                left = mid + 1     # if current smaller, must be inserting at later index
        return left   # at this point, left = right, so return either one is ok
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

The longest increasing sequence is a sorted array. Every time we find a smaller value, we replace it in longest at the right position, every time we find a larger one, we append it in longest at the very end.

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

# Increasing Triplet Subsequence

> Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

> Formally the function should:

> Return true if there exists i, j, k such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 else return false.

> Your algorithm should run in O(n) time complexity and O(1) space complexity.

> Examples:

>```
Given [1, 2, 3, 4, 5],
return true.
Given [5, 4, 3, 2, 1],
return false.
```

```Python
class Solution(object):
    def increasingTriplet(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        i, j, k = -1, -1, -1
        for idx, val in enumerate(nums):
            if i == -1 or val <= nums[i]:
                i = idx
            elif j == -1 or val <= nums[j]:
                j = idx
            else:
                return True
        return k != -1
```

```Python
class Solution(object):
    def increasingTriplet(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums) < 3:
            return False
        dp = [0] * len(nums)
        dp[0], idx = nums[0], 0
        for i in xrange(1, len(nums)):
            pos = self.binarySearch(dp, idx, nums[i])
            if dp[pos] > nums[i]: dp[pos] = nums[i]
            if pos > idx:
                idx, dp[pos] = pos, nums[i]
            if idx + 1 >= 3:
                return True
        return False
    
    def binarySearch(self, dp, idx, val):
        left, right = 0, idx
        while left <= right:
            mid = left + (right - left) / 2
            if dp[mid] == val:
                return mid
            elif dp[mid] < val:
                left = mid + 1
                if left > right:
                    return left
            else:
                right = mid - 1
                if right < left:
                    return right + 1
```

# Russian Doll Envelopes

> You have a number of envelopes with widths and heights given as a pair of integers (w, h). One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

> What is the maximum number of envelopes can you Russian doll? (put one inside other)

> Example:

> Given envelopes = [[5,4],[6,4],[6,7],[2,3]], the maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).

The idea is that after sorting the envelopes by width and if width is the same, sort the height by descending order. Then the question becomes the same as above "Longest Increasing Subsequence".

> ```
Given envelopes = [[5,4],[6,4],[6,7],[2,3]],
after sort: [[2,3],[5,4],[6,7],[6,4]]
putting [6,7] before [6,4] is the key here.
```

```Python
class Solution(object):
    def maxEnvelopes(self, envelopes):
        """
        :type envelopes: List[List[int]]
        :rtype: int
        """
        if not envelopes: return 0
        envelopes.sort(key=lambda x: (x[0], -x[1]))
        longest = [0] * len(envelopes)
        longest[0], idx = envelopes[0][1], 0
        for i, val in enumerate(envelopes, 1):
            pos = self.insert(longest, idx, val[1])
            if val[1] <= longest[pos]:
                longest[pos] = val[1]
            else:
                longest[idx+1] = val[1]
                idx += 1
        return idx + 1
    
    def insert(self, longest, end, target):
        left, right = 0, end
        while left < right:
            mid = left + (right - left) / 2
            if longest[mid] == target: return mid
            elif longest[mid] > target:
                right = mid
            else:
                left = mid + 1
        return left
```
