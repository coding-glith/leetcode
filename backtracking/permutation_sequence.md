# Permutation Sequence

> The set [1,2,3,…,n] contains a total of n! unique permutations.

> By listing and labeling all of the permutations in order,

> We get the following sequence (ie, for n = 3):

> ```
"123"
"132"
"213"
"231"
"312"
"321"
```

> Given n and k, return the kth permutation sequence.

> Note: Given n will be between 1 and 9 inclusive.

One idea is to get all the permutations then return the kth one. But we are generating too many used sequences. The idea here is to calculate the one wanted directly by appending the starting number of the sequence recursively.

```Python
class Solution(object):
    def getPermutation(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: str
        """
        # create string list
        nums = map(str, xrange(1, n+1))
        k -= 1
        # calculate (n-1)!
        factor = 1
        for i in range(1, n):
            factor *= i
        res = []
        for i in reversed(range(n)):
            res.append(nums[k / factor])
            nums.remove(nums[k / factor])
            if i != 0:
                k %= factor
                factor /= i
        return "".join(res)
```
