# Strobogrammatic Number

> A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

> Write a function to determine if a number is strobogrammatic. The number is represented as a string.

> For example, the numbers "69", "88", and "818" are all strobogrammatic.

```Python
class Solution(object):
    def isStrobogrammatic(self, num):
        """
        :type num: str
        :rtype: bool
        """
        pair = {'0': '0', '1': '1', '6': '9', '8': '8', '9': '6'}
        res = True
        for i in xrange(len(num)/2):
            print num[i], num[len(num)-1-i]
            if num[i] in pair and pair[num[i]] == num[len(num)-1-i]:
                continue
            else:
                return False
        if len(num) % 2 != 0:
            if num[len(num)/2] not in ['0', '1', '8']:
                return False
        return res
```

# Strobogrammatic Number II

> A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

> Find all strobogrammatic numbers that are of length = n.

> For example,

> Given n = 2, return ["11","69","88","96"].

> Hint:

> * Try to use recursion and notice that it should recurse with n - 2 instead of n - 1.

For recursion, need to know that:

n = 1: [0, 1, 8], odd

n = 2: [11, 69, 88, 96, 00], even

n = 3: insert odd into n = 2

n = 4: insert even into n = 2

n = 5: insert odd into n = 4

n = 6: insert even into n = 4, and so on ...

```Python
class Solution(object):
    def findStrobogrammatic(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        even = ['11', '69', '88', '96', '00']
        odd  = ['0', '1', '8']
        if n == 1:
            return odd
        if n == 2:
            return even[:-1]
        if n % 2:
            pre, mid = self.findStrobogrammatic(n-1), odd
        else:
            pre, mid = self.findStrobogrammatic(n-2), even
        idx = (n - 1) / 2
        return [p[:idx] + m + p[idx:] for m in mid for p in pre]
```
