# Repeated Substring Pattern

> Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.

> Example 1:

> ```
Input: "abab"
Output: True
Explanation: It's the substring "ab" twice.
```

> Example 2:

> ```
Input: "aba"
Output: False
```

> Example 3:

> ```
Input: "abcabcabcabc"
Output: True
Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)
```

Check leetcode [discussion](https://discuss.leetcode.com/topic/68206/easy-python-solution-with-explaination). since there must be at least one repeat pattern, if concatenate the two string and delete one char from start and end, which is deleting one pattern for each of them, there should still be string in the concatenated string. 

```Python
class Solution(object):
    def repeatedSubstringPattern(self, str):
        """
        :type str: str
        :rtype: bool
        """
        return (str + str)[1:-1].find(str) != -1
```

```Python
class Solution(object):
    def repeatedSubstringPattern(self, str):
        """
        :type str: str
        :rtype: bool
        """
        if not str: return False
        idx = 0
        for i in xrange(1, len(str)):
            if str[i] in str[:idx+1]:
                if len(str) % len(str[:idx+1]) == 0:
                    for j in xrange(i, len(str), len(str[:idx+1])):
                        if str[j:j+len(str[:idx+1])] != str[:idx+1]: break
                        else:
                            if j == len(str) - len(str[:idx+1]): return True
            idx = i
        return False
```
