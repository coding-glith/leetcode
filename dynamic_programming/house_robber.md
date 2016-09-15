# House Robber

> You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

> Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

The idea is current profit is the maximum of two previous + curNode and previous, no matter which node it chooses as long as it doesn't alarm the alert.

```Python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        if len(nums) <= 2:
            return max(nums)
        twoPrev, prev = nums[0], max(nums[0], nums[1])
        for i in xrange(2, len(nums)):
            cur = max(twoPrev + nums[i], prev)
            twoPrev, prev = prev, cur
        return prev
```

```Python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        profit = 0
        if len(nums) == 0:
            return 0
        if len(nums) == 1:
            return nums[0]
        result = [0 for i in xrange(len(nums))]
        result[0], result[1] = nums[0], max(nums[0], nums[1])
        # result represent profit with i selected
        for i in xrange(2, len(nums)):
            result[i] = max(result[i-2] + nums[i], result[i-1])
        return result[len(nums)-1]
```

# House Robber II

> Note: This is an extension of House Robber.

> After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

> Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

This idea is to calculate house robber I with max(noEndArray, noBeginArray).

```Python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        def _rob(nums):
            prev, cur = 0, 0
            for i in xrange(len(nums)):
                prev, cur = cur, max(prev + nums[i], cur)
            return cur
        noEnd, noBegin = _rob(nums[:-1]), _rob(nums[1:])
        return max(noEnd, noBegin) if len(nums) != 1 else nums[0]
```

# House Robber III

> The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

> Determine the maximum amount of money the thief can rob tonight without alerting the police.

> Example 1:

> ```
     3
    / \
   2   3
    \   \ 
     3   1
```

> Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.

> Example 2:

> ```
     3
    / \
   4   5
  / \   \ 
 1   3   1
```

> Maximum amount of money the thief can rob = 4 + 5 = 9.

Good step by step explanation from [leetcode discussion](https://discuss.leetcode.com/topic/39834/step-by-step-tackling-of-the-problem).

```Python
class Solution(object):
    def rob(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        def helper(root):
            if not root:
                return [0] * 2
            left = helper(root.left)
            right = helper(root.right)
            res = [0] * 2
            res[0] = max(left) + max(right)
            res[1] = root.val + left[0] + right[0]
            return res
        return max(helper(root))
```

Recursive, idea is easy to understand, but will get "Time Limit Exceeded".

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def rob(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root: return 0
        val = 0
        if not root.left:
            val += rob(root.left.left) + rob(root.left.right)
        if not root.right:
            val += rob(root.right.left) + rob(root.right.right)
        return max(val + root.val, rob(root.left)+rob(root.right))
```
