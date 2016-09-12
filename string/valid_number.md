# Valid Number

> Validate if a given string is numeric.

> Some examples:

> ```
"0" => true
" 0.1 " => true
"abc" => false
"1 a" => false
"2e10" => true
```

> Note: It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

The following code didn't get accepted in leetcode oj. Check the solution from leetcode [discussion](https://discuss.leetcode.com/topic/30058/a-simple-solution-in-python-based-on-dfa).

test cases:

```
"0"
" 0.2 "
" .3"
"2e10"
"2e-10"
" -0.5"
" +0.6"
"3."
"e"   ---> False
"e9" ---> False
"1e9"---> True
```

```Python
class Solution(object):
    def isNumber(self, s):
        """
        :type s: str
        :rtype: bool
        """
        idx = 0
        while idx < len(s):
            if s[idx] != " ":
                break
            idx += 1
        if idx == len(s):       # case: "    "
            return False
        if s[idx] == "-" or s[idx] == "+":    # check for sign
            idx += 1
        if idx < len(s) and s[idx] == "e":    # case: "e234"
            return False
        while idx < len(s):
            if s[idx].isdigit():
                idx += 1
            elif s[idx] == "." or s[idx] == "e":
                break
            else:
                while idx < len(s):   # check for tailor "  "
                    if s[idx] == " ":
                        idx +=1
                    else:
                        return False
        if idx < len(s):
            idx += 1
            if idx >= len(s) and s[idx-1] != ".":
                return False
        if s[idx-1] == "e":
            if s[idx] == "-" or s[idx] == "+":
                idx += 1
        while idx < len(s):
            if s[idx].isdigit():
                idx += 1
            else:
                if s[idx] == " ":
                    while idx < len(s):
                        if s[idx] == " ":
                            idx += 1
                        else:
                            return False
                    return True
                else:
                    return False
        return True  
```
