# Add Binary

> Given two binary strings, return their sum (also a binary string).

> For example,

> a = "11"

> b = "1"

> Return "100".

```Python
class Solution(object):
    def addBinary(self, a, b):
        """
        :type a: str
        :type b: str
        :rtype: str
        """
        if len(a) == 0:
            return b
        if len(b) == 0:
            return a
        i, count = 0, 0
        result = ''
        first, second = a[-1], b[-1]
        while i < len(a) or i < len(b):
            digit = int(first) + int(second) + count
            result += str(digit % 2)
            count = digit / 2
            i += 1
            if i >= len(a):
                first = '0'
            else:
                first = a[len(a)-1-i]
            if i >= len(b):
                second = '0'
            else:
                second = b[len(b)-1-i]
        if count != 0:
            result += '1'
        return result[::-1]
```
