# Reverse String

> Write a function that takes a string as input and returns the string reversed.

> Example:

> Given s = "hello", return "olleh".

Can take the advantage of Python string to use s[::-1] to get the desired results. Otherwise swap one by one. But need to change string to list because string[i] cannot be assigned directly.

```Python
class Solution(object):
    def reverseString(self, s):
        """
        :type s: str
        :rtype: str
        """
        s = list(s)
        for i in xrange(len(s)/2):
            s[i], s[len(s)-1-i] = s[len(s)-1-i], s[i]
        return ''.join(s)
```
