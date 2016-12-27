# Shortest Palindrome

> Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

> For example:

> * Given "aacecaaa", return "aaacecaaa".

> * Given "abcd", return "dcbabcd".

The idea is to check from the end of string, if the substring from 0 to i is a palindrome, then append the suffix at the beginning. However, straightforward solution gets TLE error, below solution takes advantage of using "startswith", which is faster.

```Python
class Solution(object):
    def shortestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        rev = s[::-1]
        for i in xrange(len(s)+1):
            if s.startswith(rev[i:]):
                return rev[:i] + s
        return rev[1:] + s
```

```Python
class Solution(object):
    def shortestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        for i in xrange(len(s), 0, -1):
            if s[:i] == s[:i][::-1]:
                return s[i:][::-1] + s
        return s[1:][::-1] + s
```
