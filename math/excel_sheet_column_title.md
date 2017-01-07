# Excel Sheet Column Title

> Given a positive integer, return its corresponding column title as appear in an Excel sheet.

> For example:

> ```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
```

Note: chr() Return a string of one character whose ASCII code is the integer i. For example, chr(97) returns the string 'a'. This is the inverse of ord(). The argument must be in the range [0..255], inclusive.

Solution reference from leetcode discussion [here](https://discuss.leetcode.com/topic/6245/python-solution-with-explanation)

ABCD＝A×26³＋B×26²＋C×26¹＋D＝1×26³＋2×26²＋3×26¹＋4

ZZZZ＝Z×26³＋Z×26²＋Z×26¹＋Z＝26×26³＋26×26²＋26×26¹＋26

```Python
class Solution(object):
    def convertToTitle(self, n):
        """
        :type n: int
        :rtype: str
        """
        capitals = [chr(x) for x in xrange(ord('A'), ord('Z')+1)]
        result = []
        while n > 0:
            result.append(capitals[(n-1)%26])  # n-1 because of capitals start from 0
            n = (n - 1) / 26
        result.reverse()
        return ''.join(result)
```

# Excel Sheet Column Number

> Given a column title as appear in an Excel sheet, return its corresponding column number.

> For example:

> ```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
```

```Python
class Solution(object):
    def titleToNumber(self, s):
        """
        :type s: str
        :rtype: int
        """
        capitals = {}
        for i in xrange(1, 27):
            capitals[chr(ord("A") + i - 1)] = i
        result = 0
        for char in s:
            result = result * 26 + capitals[char]
        return result
```
