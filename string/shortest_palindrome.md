# Shortest Palindrome

> Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

> For example:

> * Given "aacecaaa", return "aaacecaaa".

> * Given "abcd", return "dcbabcd".

KMP solution inspired from leetcode [discussion](https://discuss.leetcode.com/topic/27261/clean-kmp-solution-with-super-detailed-explanation). The idea is that appeding #+reversed(s), and get the kmp table for look up. so kmp[-1] is the index value of matching with prefix of the concatenated string.

> ```
             012345
for example: catacb
concatenated: catacb#bcatac # is to make sure start kmp index count at the very beginning
kmp index:   -1000000001234
which means original string s[:kmp[-1]+1] is a palindrome, so just need to append reversed(s[kmp[-1]+1:]) at the beginning.
```

```Python
class Solution(object):
    def shortestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        if not s: return s
        string = s + "#" + s[::-1]
        kmp = [-1] * len(string)
        prev, cur = -1, 0
        while cur < len(string)-1:
            if prev == -1 or string[cur] == string[prev]:
                prev += 1; cur += 1
                kmp[cur] = prev
            else:
                prev = kmp[prev]
        return s[kmp[-1]+1:][::-1] + s
```

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
