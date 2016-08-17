# Palindrome Permutation

> Given a string, determine if a permutation of the string could form a palindrome.

> For example,

> "code" -> False, "aab" -> True, "carerac" -> True.

```Python
class Solution(object):
    def canPermutePalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        return sum(i % 2 for i in collections.Counter(s).values()) < 2
```
