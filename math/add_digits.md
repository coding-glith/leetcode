# Add Digits

> Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

> For example:

> Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

> Follow up:

> Could you do it without any loop/recursion in O(1) runtime?

Besides above step by step method, wikipedia has an explanation for ["digit root"](https://en.wikipedia.org/wiki/Digital_root).

```Python
class Solution(object):
    def addDigits(self, num):
        """
        :type num: int
        :rtype: int
        """
        if num == 0:
            return 0
        result = 0
        while 1:
            result += num % 10
            num /= 10
            if num == 0:
                if result / 10 == 0:
                    break
                else:
                    num = result
                    result = 0
        return result
```
