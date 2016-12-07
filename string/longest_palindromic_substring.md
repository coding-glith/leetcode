# Longest Palindromic Substring

> Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

> Example:

> ```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

> Example:

> ```
Input: "cbbd"
Output: "bb"
```

The idea is to go through the string, add try to add the character, or add the character and the character before the current string to see if can form palindrome.

For example, for babad, if current is aba and we are checking d, then we will check abad and babad.

```Python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        def isPalindrome(start, end):
            if start < 0 or end >= len(s) or start > end: return False
            while start <= end:
                if s[start] != s[end]: return False
                start += 1; end -= 1
            return True
        
        res, curLen = "", 0
        for i in xrange(len(s)):
            if isPalindrome(i-curLen-1, i):   # add s[i] and s[i-curLen-1]
                res, curLen = s[i-curLen-1:i+1], curLen + 2
            elif isPalindrome(i-curLen, i):   # add s[i]
                res, curLen = s[i-curLen:i+1], curLen + 1
        return res
```
