# Letter Combinations of a Phone Number

> Given a digit string, return all possible letter combinations that the number could represent.

> A mapping of digit to letters (just like on the telephone buttons) is given below.

> ![alt text](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

> ```
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

> Note:

> Although the above answer is in lexicographical order, your answer could be in any order you want.

Be very clear of the key of the dictionary and digits index to do the iteration.

```Python
class Solution(object):
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        if digits == '':
            return []
        # create mapping dictionary
        letterDict = {}
        letterDict['0'] = ['']
        letterDict['1'] = ['']
        letterDict['2'] = ['a', 'b', 'c']
        letterDict['3'] = ['d', 'e', 'f']
        letterDict['4'] = ['g', 'h', 'i']
        letterDict['5'] = ['j', 'k', 'l']
        letterDict['6'] = ['m', 'n', 'o']
        letterDict['7'] = ['p', 'q', 'r', 's']
        letterDict['8'] = ['t', 'u', 'v']
        letterDict['9'] = ['w', 'x', 'y', 'z']
        result = []
        self.letterCombine(result, '', 0, letterDict, digits)
        return result

    def letterCombine(self, result, combineStr, digitIndx, letterDict, digits):
        if len(combineStr) == len(digits) and combineStr not in result:
            result.append(str(combineStr))
            return
        dictKey = digits[digitIndx]
        for indx in range(len(letterDict[dictKey])):
            combineStr += letterDict[dictKey][indx]
            self.letterCombine(result, combineStr, digitIndx + 1, letterDict, digits)
            combineStr = combineStr[:-1]
```
