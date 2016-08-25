# Reverse Words in a String

> Given an input string, reverse the string word by word.

> For example,

> Given s = "the sky is blue",

> return "blue is sky the".

> Clarification:

> What constitutes a word?

> A sequence of non-space characters constitutes a word.

> Could the input string contain leading or trailing spaces?

> Yes. However, your reversed string should not contain leading or trailing spaces.

> How about multiple spaces between two words?

> Reduce them to a single space in the reversed string.

Test cases: "", " ", "    ", "  1   ", "hello   world".

```Python
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        if not s:
            return s
        d, w = [], ""
        s += " "
        for i in xrange(len(s)):
            if s[i] != " ":
                w += s[i]
            elif s[i] == " " and w != "":
                d.append(w)
                w = ""
        if not d:
            return ""
        res = ""
        for i in xrange(len(d)-1, -1, -1):
            if i != 0:
                res += d[i] + " "
            else:
                res += d[i]
        return res
```
