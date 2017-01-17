# Different Ways to Add Parentheses](different_ways_to_add_parentheses.md)

> Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are +, - and *.

> Example 1

> ```
Input: "2-1-1".
((2-1)-1) = 0
(2-(1-1)) = 2
Output: [0, 2]
```

> Example 2

> ```
Input: "2*3-4*5"
(2*(3-(4*5))) = -34
((2*3)-(4*5)) = -14
((2*(3-4))*5) = -10
(2*((3-4)*5)) = -10
(((2*3)-4)*5) = 10
Output: [-34, -14, -10, -10, 10]
```

```Python
class Solution(object):
    def diffWaysToCompute(self, input):
        """
        :type input: str
        :rtype: List[int]
        """
        if input.isdigit(): return [int(input)]
        result = []
        for i in xrange(len(input)):
            if input[i] in ["+", "-", "*"]:
                left = self.diffWaysToCompute(input[:i])
                right = self.diffWaysToCompute(input[i+1:])
                for part1 in left:
                    for part2 in right:
                        result.append(self.helper(part1, part2, input[i]))
        return result
    
    def helper(self, val1, val2, operator):
        if operator == "+": return val1 + val2
        elif operator == "-": return val1 - val2
        else: return val1 * val2
```
