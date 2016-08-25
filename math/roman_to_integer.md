# Roman to Integer

> Given a roman numeral, convert it to an integer.

> Input is guaranteed to be within the range from 1 to 3999.

Need to understand the form of [roman numerals](https://en.wikipedia.org/wiki/Roman_numerals).

```Python
class Solution(object):
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        d = {'M':1000, 'D':500, 'C':100, 'L':50, 'X':10, 'V':5, 'I':1}
        res, p = 0, 'I'
        for c in s[::-1]:
            res, p = res - d[c] if d[c] < d[p] else res + d[c], c
        return res
```

# Integer to Roman

> Given an integer, convert it to a roman numeral.

> Input is guaranteed to be within the range from 1 to 3999.

```Python
class Solution(object):
    def intToRoman(self, num):
        """
        :type num: int
        :rtype: str
        """
        symbols = ["M", "D", "C", "L", "X", "V", "I"]
        M = ["", "M", "MM", "MMM"]
        C = ["", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"]
        X = ["", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"]
        I = ["", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"]
        return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10]
```
