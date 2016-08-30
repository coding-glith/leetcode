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

# Palindrome Permutation II

> Given a string s, return all the palindromic permutations (without duplicates) of it. Return an empty list if no palindromic permutation could be form.

> For example:

> Given s = "aabb", return ["abba", "baab"].

> Given s = "abc", return [].

> Hint:

> * If a palindromic permutation exists, we just need to generate the first half of the string.

> * To generate all distinct permutations of a (half of) string, use a similar approach from: Permutations II or Next Permutation.

```Python

```
