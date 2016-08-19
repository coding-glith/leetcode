# Unique Word Abbreviation

> An abbreviation of a word follows the form <first letter><number><last letter>. Below are some examples of word abbreviations:

> ```
a) it                      --> it    (no abbreviation)
     1
b) d|o|g                   --> d1g
              1    1  1
     1---5----0----5--8
c) i|nternationalizatio|n  --> i18n
              1
     1---5----0
d) l|ocalizatio|n          --> l10n
```

> Assume you have a dictionary and given a word, find whether its abbreviation is unique in the dictionary. A word's abbreviation is unique if no other word from the dictionary has the same abbreviation.

> Example:

> ```
Given dictionary = [ "deer", "door", "cake", "card" ]
isUnique("dear") -> false
isUnique("cart") -> true
isUnique("cane") -> false
isUnique("make") -> true
```

```Python
class ValidWordAbbr(object):
    def __init__(self, dictionary):
        """
        initialize your data structure here.
        :type dictionary: List[str]
        """
        self.abbr = {}
        for elem in dictionary:
            if self.getAbbr(elem) not in self.abbr:
                self.abbr[self.getAbbr(elem)] = [elem]
            else:
                if elem not in self.abbr[self.getAbbr(elem)]:
                    self.abbr[self.getAbbr(elem)].append(elem)

    def isUnique(self, word):
        """
        check if a word is unique.
        :type word: str
        :rtype: bool
        """
        if self.getAbbr(word) not in self.abbr:
            return True
        if self.abbr[self.getAbbr(word)] == [word]:
            return True
        return False

    def getAbbr(self, s):
        if len(s) <= 1:
            return s
        else:
            return s[0] + str(len(s)-2) + s[-1]
        


# Your ValidWordAbbr object will be instantiated and called as such:
# vwa = ValidWordAbbr(dictionary)
# vwa.isUnique("word")
# vwa.isUnique("anotherWord")
```
