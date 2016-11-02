# Range Sum Query - Immutable

> Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

> Example:

> ```
Given nums = [-2, 0, 3, -5, 2, -1]
sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```

> Note:

> * You may assume that the array does not change.

> * There are many calls to sumRange function.

The idea of this question is to get the results efficiently. So if we store all the sums up to j, then we don't need to do addition every time.

```Python
class NumArray(object):
    def __init__(self, nums):
        """
        initialize your data structure here.
        :type nums: List[int]
        """
        self.nums = list(nums)
        for i in xrange(1, len(nums)):
            nums[i] += nums[i-1]
        self.numsSum = nums

    def sumRange(self, i, j):
        """
        sum of elements nums[i..j], inclusive.
        :type i: int
        :type j: int
        :rtype: int
        """
        return self.numsSum[j]-self.numsSum[i]+self.nums[i]
        


# Your NumArray object will be instantiated and called as such:
# numArray = NumArray(nums)
# numArray.sumRange(0, 1)
# numArray.sumRange(1, 2)
```

# Range Sum Query - Mutable

> Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

> The update(i, val) function modifies nums by updating the element at index i to val.

> Example:

> ```
Given nums = [1, 3, 5]
sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```

> Note:

> * The array is only modifiable by the update function.

> * You may assume the number of calls to update and sumRange function is distributed evenly.

```Python

```
