# Palindrome Partitioning

> Given a string s, partition s such that every substring of the partition is a palindrome.

> Return all possible palindrome partitioning of s.

> For example, given s = "aab",

> Return

> ```
[
  ["aa","b"],
  ["a","a","b"]
]
```

```Python
class Solution(object):
    def partition(self, s):
        """
        :type s: str
        :rtype: List[List[str]]
        """
        if not s:
            return []
        res = []
        self.helper(res, [], 0, s)
        return res

    def isPalindrome(self, s):
        if not s:
            return False
        if len(s) == 1:
            return True
        start, end = 0, len(s) - 1
        while start < end:
            if s[start] != s[end]:
                return False
            start += 1
            end -= 1
        return True

    def helper(self, res, sub, idx, s):
        if len(sub) > 0 and idx == len(s):
            res.append(list(sub))
            return
        for i in xrange(len(s)):
            if self.isPalindrome(s[idx:i+1]):
                sub.append(s[idx:i+1])
                self.helper(res, sub, i+1, s)
                sub.pop()
```
