# Plus One

> Given a non-negative number represented as an array of digits, plus one to the number.

> The digits are stored such that the most significant digit is at the head of the list.

For digits = [9], needs to insert one element at the beginning of array.

```Python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        carry = 1
        for i in xrange(len(digits)-1, -1, -1):
            digits[i], carry = (digits[i] + carry) % 10, (digits[i] + carry) / 10
        if carry == 1:
            digits.insert(0, carry)
        return digits
```
