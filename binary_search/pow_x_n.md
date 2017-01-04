# Pow(x, n)

> Implement pow(x, n).

```Python
class Solution(object):
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        if not n:
            return 1
        if n < 0:
            return 1 / self.myPow(x, -n)
        if n % 2:
            return x * self.myPow(x, n-1)
        return self.myPow(x*x, n/2)
```

# Super Pow

> Your task is to calculate ab mod 1337 where a is a positive integer and b is an extremely large positive integer given in the form of an array.

> Example1:

> ```
a = 2
b = [3]
Result: 8
```
> Example2:

> ```
a = 2
b = [1,0]
Result: 1024
```

need to understand this: ab % k = (a%k)(b%k)%k. check Leetcode [discussion](https://discuss.leetcode.com/topic/50489/c-clean-and-short-solution)

```Python
class Solution(object):
    def superPow(self, a, b):
        """
        :type a: int
        :type b: List[int]
        :rtype: int
        """
    def __init__(self):
        self.base = 1337

    def powMod(self, a, k):
        a, res = a % self.base, 1
        for i in xrange(0, k):
            res = (res * a) % self.base
        return res
        
    def superPow(self, a, b):
        if not b:
            return 1
        last = b.pop()
        return self.powMod(self.superPow(a, b), 10) * self.powMod(a, last) % self.base  
```
