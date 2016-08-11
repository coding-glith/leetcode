# Length of Last Word

> Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

> If the last word does not exist, return 0.

> Note: A word is defined as a character sequence consists of non-space characters only.

> For example, 

> Given s = "Hello World",

> return 5.

Need to consider different cases like "", " ", "       ", "  a  b", "a  b     ", etc.

```Python
class Solution(object):
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """
        if s == "" or s == " ":
            return 0
        last = s[0]
        for indx in xrange(1, len(s)):
            if s[indx] != " ":
                if s[indx-1] != " ":
                    last += s[indx]
                else:
                    last = s[indx]
        if last == " ":
            return 0
        return len(last)
```
