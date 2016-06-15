# Two Sum

> Given an array of integers, return indices of the two numbers such that they add up to a specific target.

> You may assume that each input would have exactly one solution.

> Example:

> ```
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

```Python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        dict = {}
        for indx in xrange(len(nums)):
            if dict.has_key(target - nums[indx]):
                return [dict[target - nums[indx]], indx]
            else:
                dict[nums[indx]] = indx
        return []
```

# Two Sum II - Input array is sorted

> Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

> The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned 

> answers (both index1 and index2) are not zero-based.

> You may assume that each input would have exactly one solution.

> Input: numbers={2, 7, 11, 15}, target=9

> Output: index1=1, index2=2

Using dictionary, same as above.

```Python
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        dict = {}
        for indx in xrange(len(numbers)):
            if dict.has_key(target - numbers[indx]):
                return [dict[target - numbers[indx]]+1, indx+1]
            else:
                dict[numbers[indx]] = indx
        return []
```

# Two Sum III - Data structure design

> Design and implement a TwoSum class. It should support the following operations: add and find.

> add - Add the number to an internal data structure.

> find - Find if there exists any pair of numbers which sum is equal to the value.

> For example,

> ```
add(1); add(3); add(5);
find(4) -> true
find(7) -> false
```

Needs to consider unique key cases and duplicate keys cases.

```Python
class TwoSum(object):

    def __init__(self):
        """
        initialize your data structure here
        """
        self.nums = {}
        

    def add(self, number):
        """
        Add the number to an internal data structure.
        :rtype: nothing
        """
        if number not in self.nums:
            self.nums[number] = 1   # key is the number, value if the count of the number
        else:
            self.nums[number] += 1
        

    def find(self, value):
        """
        Find if there exists any pair of numbers which sum is equal to the value.
        :type value: int
        :rtype: bool
        """
        for key in self.nums:
            if value - key in self.nums and (value - key != key or self.nums[key] > 1):
                return True
        return False
        

# Your TwoSum object will be instantiated and called as such:
# twoSum = TwoSum()
# twoSum.add(number)
# twoSum.find(value)
```

#
