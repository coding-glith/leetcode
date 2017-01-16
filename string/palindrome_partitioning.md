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

# Palindrome Partitioning II

> Given a string s, partition s such that every substring of the partition is a palindrome.

> Return the minimum cuts needed for a palindrome partitioning of s.

> For example, given s = "aab",

> Return 1 since the palindrome partitioning ["aa","b"] could be produced using 1 cut.

From leetcode [discussion](https://discuss.leetcode.com/topic/2840/my-solution-does-not-need-a-table-for-palindrome-is-it-right-it-uses-only-o-n-space). O(N^2) solution, go through the string, and check its left and right to find the max palindrome with current index as center, then update the dp status.

```Python
class Solution(object):
    def minCut(self, s):
        """
        :type s: str
        :rtype: int
        """
        dp = [0] * (len(s)+1)
        for i in xrange(len(s)+1):
            dp[i] = i - 1
        for i in xrange(len(s)):   # j is the radius from i to left and right
            for j in xrange(i+1):   # odd case
                if i+j >= len(s) or s[i-j] != s[i+j]: break
                dp[i+j+1] = min(dp[i+j+1], dp[i-j]+1)
            for j in xrange(1, i+2):  # even case
                if i+j >= len(s) or s[i-j+1] != s[i+j]: break
                dp[i+j+1] = min(dp[i+j+1], dp[i-j+1]+1)
        return dp[-1]
```
