# Sum of Two Integers

> Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

> Example:

> Given a = 1 and b = 2, return 3.

Review python [bitwise operations](http://www.tutorialspoint.com/python/bitwise_operators_example.htm). Not quite clear yet. :-(

```Python
class Solution(object):
    def getSum(self, a, b):
        """
        :type a: int
        :type b: int
        :rtype: int
        """
        # 32 bits integer max
        MAX = 0x7FFFFFFF
        # 32 bits integer min
        MIN = 0x80000000
        # mask to get last 32 bits
        mask = 0xFFFFFFFF
        while b != 0:
            # ^ get different bits (XOR)
            # & get two 1s
            # << move carry
            a, b = (a ^ b) & mask, ((a & b) << 1) & mask
            # if a is negative, get a's 32 bits complement positive first
            # then get 32 bit positive's python complement negative
        return a if a <= MAX else ~(a ^ mask)
```
