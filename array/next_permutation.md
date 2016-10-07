# Next Permutation

> Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

> If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

> The replacement must be in-place, do not allocate extra memory.

> Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

> ```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

Check explanation from [here](https://www.nayuki.io/page/next-lexicographical-permutation-algorithm).

```Python
class Solution(object):
    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        if len(nums) <= 1: return
        piv = -1  # from end to start, piv is the first elem smaller than local peak
        for i in xrange(len(nums)-1, 0, -1):
            if nums[i] > nums[i-1]:
                piv = i - 1
                break
        if piv == -1:   # maximum permutation sequence
            nums.reverse()
            return
        for i in xrange(len(nums)-1, piv, -1):
            if nums[i] > nums[piv]:
                nums[i], nums[piv] = nums[piv], nums[i]
                break
        nums[piv+1:] = nums[piv+1:][::-1]   # the sequence after piv is in decreasing order, need to reverse to inceasing order
```
