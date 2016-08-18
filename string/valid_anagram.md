# Valid Anagram

> Given two strings s and t, write a function to determine if t is an anagram of s.

> For example,

> s = "anagram", t = "nagaram", return true.

> s = "rat", t = "car", return false.

> Note:

> You may assume the string contains only lowercase alphabets.

> Follow up:

> What if the inputs contain unicode characters? How would you adapt your solution to such case?

```Python
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        alphaDict = {chr(x) : 0 for x in xrange(ord('a'), ord('z')+1)}
        for i in s:
            alphaDict[i] += 1
        for j in t:
            alphaDict[j] -= 1
            if alphaDict[j] < 0:
                return False
        for x in alphaDict.values():
            if x != 0:
                return False
        return True
```
