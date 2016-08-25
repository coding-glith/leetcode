# Fraction to Recurring Decimal

> Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

> If the fractional part is repeating, enclose the repeating part in parentheses.

> For example,

> * Given numerator = 1, denominator = 2, return "0.5".

> * Given numerator = 2, denominator = 1, return "2".

> * Given numerator = 2, denominator = 3, return "0.(6)".

> Hint:

> * No scary math, just apply elementary math knowledge. Still remember how to perform a long division?

> * Try a long division on 4/9, the repeating part is obvious. Now try 4/333. Do you see a pattern?

> * Be wary of edge cases! List out as many test cases as you can think of and test your code thoroughly.

Cases to be considered: -4/333; 4/9; 4/2; 3/8; 36/5; 9/7.

```Python
class Solution(object):
    def fractionToDecimal(self, numerator, denominator):
        """
        :type numerator: int
        :type denominator: int
        :rtype: str
        """
        n, remainder = divmod(abs(numerator), abs(denominator))
        sign = '-' if numerator * denominator < 0 else ''
        res, stack = [sign + str(n), '.'], []
        while remainder not in stack:
            stack.append(remainder)
            n, remainder = divmod(remainder*10, abs(denominator))
            res.append(str(n))
        idx = stack.index(remainder)
        res.insert(idx+2, '(')
        res.append(')')
        return ''.join(res).replace('(0)', '').rstrip('.')
```
