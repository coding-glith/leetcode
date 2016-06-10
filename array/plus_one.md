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
        for index in xrange(-1, -len(digits)-1, -1):
            flag = (digits[index] + 1) / 10
            digits[index] = (digits[index] + 1) % 10
            if flag == 0:
                break
        if index == -len(digits) and flag != 0:
            digits.insert(0,1)
        return digits
```
