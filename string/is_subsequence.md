# Is Subsequence

> Given a string s and a string t, check if s is subsequence of t.

> You may assume that there is only lower case English letters in both s and t. t is potentially a very long (length ~= 500,000) string, and s is a short string (<=100).

> A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ace" is a subsequence of "abcde" while "aec" is not).

> ```
Example 1:
s = "abc", t = "ahbgdc"
Return true.
Example 2:
s = "axc", t = "ahbgdc"
Return false.
```

> Follow up:

> If there are lots of incoming S, say S1, S2, ... , Sk where k >= 1B, and you want to check one by one to see if T has its subsequence. In this scenario, how would you change your code?

O(len(t)) complexity.

```Python
class Solution(object):
    def isSubsequence(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        if not s: return True
        if len(s) > len(t): return False
        si, ti = 0, 0
        while si < len(s) and ti < len(t):
            if s[si] == t[ti]:
                if si == len(s) - 1: return True
                si += 1
                ti += 1
            else:
                ti += 1
        return False
```

Another idea is use a dictionary to search for the index of t's characters. O(len(s) * log(len(t))) complexity. But in oj, it gets Time Limit Exceeded.

```Python
class Solution(object):
    def isSubsequence(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        if not s: return True
        if len(s) > len(t): return False
        # create a dictionary of characters in t
        tDict = {}
        for i in xrange(len(t)):
            tDict[t[i]] = tDict.get(t[i], []) + [i]
        # check for s
        pos = 0
        for i in xrange(len(s)):
            if s[i] not in tDict: return False
            pos = self.binarySearch(tDict[s[i]], pos)
            if pos == -1:
                return False
        return True

    def binarySearch(self, array, target):
        left, right, cmpIdx = 0, len(array)-1, -1
        while left <= right:
            mid = left + (right - left) / 2
            if array[mid] == target:
                cmpIdx = mid
                break
            elif array[mid] < target:
                left = mid + 1
                if left > right:
                    cmpIdx = left
            else:
                right = mid - 1
                if right < left:
                    cmpIdx = right + 1
        if cmpIdx == -1 or cmpIdx >= len(array):
            return -1
        else:
            return array[cmpIdx] + 1
```
