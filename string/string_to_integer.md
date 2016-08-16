# String to Integer (atoi)

> Implement atoi to convert a string to an integer.

Only ' +324   %23' will be accepted as '324'; need to deal with space, sign, other symbols and overflow.

```Python
class Solution(object):
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        sign, base, i = 1, 0, 0
        while i < len(str) and str[i] == " ":
            i += 1
        if i < len(str) and str[i] in ['-', '+']:
            sign = -1 if str[i] == '-' else 1
            i += 1
        while i < len(str) and str[i] >= '0' and str[i] <= '9':
            if base > 214748364 or (base == 214748364 and int(str[i]) > 7):
                if sign == 1:
                    return 2147483647
                else:
                    return -2147483648
            base = base * 10 + int(str[i])
            i += 1
        return sign * base
```
