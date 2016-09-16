# Counting Bits

> Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

> Example:

> For num = 5 you should return [0,1,1,2,1,2].

> Follow up:

> * It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?

> * Space complexity should be O(n).

> * Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

> Hint:

> * You should make use of what you have produced already.

> * Divide the numbers in ranges like [2-3], [4-7], [8-15] and so on. And try to generate new range from previous.

> * Or does the odd/even status of the number help you in calculating the number of 1s?

```
0                 0
1                 1  ---
2                10    |
3                11    |
4               100    |
5               101    +1
6               110    |
7               111    |
8              1000    |
9              1001  ---
```

```Python
class Solution(object):
    def countBits(self, num):
        """
        :type num: int
        :rtype: List[int]
        """
        res = [0]
        i, window, count = 1, 1, 1
        while i <= num:
            res.append(1 + res[i-window])
            if count == window:
                window *= 2
                count = 1
            i += 1
            count += 1
        return res
```
