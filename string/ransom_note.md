# Ransom Note

> Given an arbitrary ransom note string and another string containing letters from all the magazines,
write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

> Each letter in the magazine string can only be used once in your ransom note.

> Note:

> You may assume that both strings contain only lowercase letters.

> ```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

This method is taking advantage of Python count() method. However, there are other ways to solve this problem: sort the string and compare one by one; maintain an array "visited", and check every character.

```Python
class Solution(object):
    def canConstruct(self, ransomNote, magazine):
        """
        :type ransomNote: str
        :type magazine: str
        :rtype: bool
        """
        if len(ransomNote) > len(magazine):
            return False
        for indx in xrange(len(ransomNote)):
            if ransomNote.count(ransomNote[indx]) > magazine.count(ransomNote[indx]):
                return False
        return True
```
