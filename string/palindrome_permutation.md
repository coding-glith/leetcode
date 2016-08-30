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
class Solution(object):
    def generatePalindromes(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        # check if can generate palindrome
        if sum(i%2 for i in collections.Counter(s).values()) >= 2:
            return []
        # get the list for prefix combination
        count = collections.Counter(s)
        sList, odd = [], ''
        for elem in count:
            if count[elem] % 2 == 1:
                odd = elem
            tmp = count[elem] / 2
            while tmp:
                sList.append(elem)
                tmp -= 1
        # prefix combination
        prefix = []
        visited = [0] * len(sList)
        sList.sort()
        self.generate(prefix, [], visited, sList)
        res = []
        for p in prefix:
            res.append(str(p+odd+p[::-1]))
        return res

    def generate(self, prefix, sub, visited, sList):
        if len(sub) == len(sList):
            prefix.append(''.join(sub))
            return
        for i in xrange(len(sList)):
            if visited[i] == 1 or (i != 0 and sList[i] == sList[i-1] and visited[i-1] == 0):
                continue
            sub.append(sList[i])
            visited[i] = 1
            self.generate(prefix, sub, visited, sList)
            sub.pop()
            visited[i] = 0
```
