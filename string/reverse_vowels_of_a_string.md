# Reverse Vowels of a String

> Write a function that takes a string as input and reverse only the vowels of a string.

> Example 1:

> Given s = "hello", return "holle".

> Example 2:

> Given s = "leetcode", return "leotcede".

> Note:

> The vowels does not include the letter "y".

```Python
class Solution(object):
    def reverseVowels(self, s):
        """
        :type s: str
        :rtype: str
        """
        if not s:
            return ""
        vowels = ['a', 'e', 'i', 'o', 'u']
        res = list(s)
        head, tail = 0, len(res)-1
        while head <= tail:
            if res[head].lower() not in vowels:
                head += 1
            elif res[tail].lower() not in vowels:
                tail -= 1
            else:
                tmp = res[head]
                res[head], res[tail] = res[tail], tmp
                head += 1
                tail -= 1
        return ''.join(res)
```
