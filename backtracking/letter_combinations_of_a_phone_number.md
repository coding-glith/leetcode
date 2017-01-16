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
        if not digits: return []
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
        self.helper(result, [], 0, digits, letterDict)
        return result
    
    def helper(self, result, sub, idx, digits, letterDict):
        if len(sub) == len(digits): result.append("".join(sub)); return
        for val in letterDict[digits[idx]]:
            sub.append(val)
            self.helper(result, sub, idx+1, digits, letterDict)
            sub.pop()
```
