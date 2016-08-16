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
