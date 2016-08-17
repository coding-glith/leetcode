# Count and Say

> The count-and-say sequence is the sequence of integers beginning as follows:

> 1, 11, 21, 1211, 111221, ...

> 1 is read off as "one 1" or 11.

> 11 is read off as "two 1s" or 21.

> 21 is read off as "one 2, then one 1" or 1211.

> Given an integer n, generate the nth sequence.

> Note: The sequence of integers will be represented as a string.

```Python
class Solution(object):
    def countAndSay(self, n):
        """
        :type n: int
        :rtype: str
        """
        if n <= 0:
            return ""
        if n== 1:
            return "1"
        res, seq = "", "1"
        while n > 0:
            tmp, count = seq[0], 0
            for i in xrange(0, len(seq)):
                if seq[i] == tmp:
                    count += 1
                else:
                    res += str(count) + seq[i-1]
                    tmp, count = seq[i], 1
            res += str(count) + seq[i]
            n -= 1
            if n == 1:
                break
            else:
                seq, res, count = res, "", 0
        return res
```
