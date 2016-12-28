# Longest Palindrome

> Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

> This is case sensitive, for example "Aa" is not considered a palindrome here.

> Note:

> Assume the length of given string will not exceed 1,010.

> Example:

> ```
Input:
"abccccdd"
Output:
7
Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```

```Python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: int
        """
        oddFlag, result = 0, 0
        for i in collections.Counter(s).values():
            if i % 2 == 0:
                result += i
            else:
                oddFlag = 1
                result += i - 1
        return result + oddFlag
```
