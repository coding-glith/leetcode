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

This solution take advantage of the split() function.

```Python
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        sSplit, res = s.split(" "), ""
        for i in xrange(len(sSplit)-1, -1, -1):
            if sSplit[i]:
                res = sSplit[i] if not res else res + " " + sSplit[i]
        return res
```

The key for this solution is how to deal with empty spaces.

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

# Reverse Words in a String II

> Given an input string, reverse the string word by word. A word is defined as a sequence of non-space characters.

> The input string does not contain leading or trailing spaces and the words are always separated by a single space.

> For example,

> Given s = "the sky is blue",

> return "blue is sky the".

> Could you do it in-place without allocating extra space?

```Python
class Solution:
    # @param s, a list of 1 length strings, e.g., s = ['h','e','l','l','o']
    # @return nothing
    def reverseWords(self, s):
        s.reverse()  # first reverse the whole string
        start = 0
        for i in xrange(len(s)):
            if s[i] == " ":
                s[start:i] = reversed(s[start:i])  # reverse the word back to normal
                start = i + 1
        s[start:] = reversed(s[start:])
```
