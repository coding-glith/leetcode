# Valid Palindrome

> Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

> For example,

> "A man, a plan, a canal: Panama" is a palindrome.

> "race a car" is not a palindrome.

> Note:

> Have you consider that the string might be empty? This is a good question to ask during an interview.

> For the purpose of this problem, we define empty string as valid palindrome.

```Python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        if not s:
            return True
        alphNum = [chr(x) for x in xrange(ord('a'), ord('z')+1)] + \
                  [chr(x) for x in xrange(ord('0'), ord('9')+1)]
        head, tail = 0, len(s)-1
        while head <= tail:
            if s[head].lower() not in alphNum:
                head += 1
            elif s[tail].lower() not in alphNum:
                tail -= 1
            else:
                if s[head].lower() != s[tail].lower():
                    return False
                else:
                    head += 1
                    tail -= 1
        return True
```
