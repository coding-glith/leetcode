# Longest Substring Without Repeating Characters

> Given a string, find the length of the longest substring without repeating characters.

> Examples:

> Given "abcabcbb", the answer is "abc", which the length is 3.

> Given "bbbbb", the answer is "b", with the length of 1.

> Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

```Python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        res, unique = 0, []
        for i in xrange(len(s)):
            if s[i] in unique:
                res = max(res, len(unique))
                for tmp in xrange(len(unique)):
                    if unique[tmp] == s[i]:
                        unique = unique[tmp+1:]
                        unique.append(s[i])
                        break
            else:
                unique.append(s[i])
        return max(res, len(unique))
```

Using two pointers.

```Python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        if len(s) <= 1: return len(s)
        res, start, end = 1, 0, 0
        for i in xrange(1, len(s)):
            if s[i] in s[start : end + 1]:
                while start <= end and s[start] != s[i]:
                    start += 1
                start += 1
            end = i
            res = max(res, end + 1 - start) 
        return res  
```
