# Multiply Strings

> Given two numbers represented as strings, return multiplication of the numbers as a string.

> Note:

> * The numbers can be arbitrarily large and are non-negative.

> * Converting the input string to integer is NOT allowed.

> * You should NOT use internal library such as BigInteger.

return is string, no need to take care of overflow.

```Python
class Solution(object):
    def multiply(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        """
        res = [0] * (len(num1) + len(num2))
        for i, e1 in enumerate(reversed(num1)):
            for j, e2 in enumerate(reversed(num2)):
                res[i+j] += int(e1) * int(e2)
                res[i+j+1] += res[i+j] /10
                res[i+j] %= 10
        while len(res) > 1 and res[-1] == 0:
            res.pop()
        return ''.join(map(str, res[::-1]))
```
