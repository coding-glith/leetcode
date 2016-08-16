# Count Primes

> Count the number of prime numbers less than a non-negative number, n.

Check explanations from [leetcode](https://leetcode.com/problems/count-primes/).

```Python

```

Straightforward solution, define isPrime() function and calculate. O(n**1.5)

```Python
class Solution(object):
    def countPrimes(self, n):
        """
        :type n: int
        :rtype: int
        """
        count = 0
        for i in xrange(1, n):
            if self.isPrime(i):
                count += 1
        return count

    def isPrime(self, n):
        if n <= 1:
            return False
        num = 2
        while num * num <= n:
            if n % num == 0:
                return False
            num += 1
        return True
```
