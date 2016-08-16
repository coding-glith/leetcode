# Power of Two

> Given an integer, write a function to determine if it is a power of two.

```Python
class Solution(object):
    def isPowerOfTwo(self, n):
        """
        :type n: int
        :rtype: bool
        """
        if n <= 0:
            return False
        while n:
            if n != 1 and n % 2 != 0:
                return False
            n /= 2
        return True
```

# Power of Three

> Given an integer, write a function to determine if it is a power of three.

> Follow up:

> Could you do it without using any loop / recursion?

We can use similar solution above, but here, we take advantage that log10(3^n) = n*log10(3).

```Python
class Solution(object):
    def isPowerOfThree(self, n):
        """
        :type n: int
        :rtype: bool
        """
        if n <= 0:
            return False
        tmp = math.log10(n) / math.log10(3)
        if tmp.is_integer():
            return True
        return False
```
