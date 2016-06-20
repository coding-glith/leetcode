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

# 3Sum

> Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

> Note: The solution set must not contain duplicate triplets.

> ```
For example, given array S = [-1, 0, 1, 2, -1, -4],
A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

Solution 1: O(n^2), fix one value, then use two pointers to find possible combination.

```Python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) <= 2:
            return []
        nums.sort()
        result = set()   # ensure no duplicate result
        for indx, val in enumerate(nums[:-2]):   # leave the last two elems
            left, right = indx + 1, len(nums) - 1   # two pointers
            while left < right:
                if nums[left] + nums[right] + val == 0:
                    result.add((val, nums[left], nums[right]))
                    left += 1
                elif val + nums[left] + nums[right] < 0:
                    left += 1
                else:
                    right -= 1
        return map(list, result)
```

Solution 2: fix one value, use dictionary to better find the other two combinations.

```Python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) <= 2:
            return []
        nums.sort()
        result = set()   # ensure no duplicate result
        for indx, val in enumerate(nums[:-2]):   # leave the last two elems
            dic = {}  # dic contains the waiting value to find a pair
            for innerVal in nums[indx+1:]:  # now the goal is to find combination of -val
                if innerVal in dic:   # means innerVal == -val - innerVal  -> reach the goal to find -val
                    result.add((val, innerVal, -val - innerVal))
                else:
                    dic[-val - innerVal] = 1
        return map(list, result)
```

# 3Sum Closest

> Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

> ```
For example, given array S = {-1 2 1 -4}, and target = 1.
The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

```Python
class Solution(object):
    def threeSumClosest(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if len(nums) <= 2:
            return []
        nums.sort()
        result = nums[0] + nums[1] + nums[2]
        for indx, val in enumerate(nums[:-2]):
            left, right = indx + 1, len(nums)-1
            while left < right:
                total = val + nums[left] + nums[right]
                if abs(target - total) < abs(target - result):
                    result = total
                if total < target:
                    left += 1
                else:
                    right -= 1
        return result
```

# 3Sum Smaller

> Given an array of n integers nums and a target, find the number of index triplets i, j, k with 0 <= i < j < k < n that satisfy the condition nums[i] + nums[j] + nums[k] < target.

> For example, given nums = [-2, 0, 1, 3], and target = 2.

> Return 2. Because there are two triplets which sums are less than 2:

> ```
[-2, 0, 1]
[-2, 0, 3]
```

> Follow up: Could you solve it in O(n^2) runtime?

```Python
class Solution(object):
    def threeSumSmaller(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if len(nums) <= 2:
            return 0
        nums.sort()
        result = 0
        for indx, val in enumerate(nums[:-2]):
            left, right = indx + 1, len(nums) -1
            while left < right:
                total = val + nums[left] + nums[right]
                if total < target:
                    result += right -left
                    left += 1
                else:
                    right -= 1
        return result
```

# 4Sum

> Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

> Note: The solution set must not contain duplicate quadruplets.

> ```
For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.
A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

```Python
class Solution(object):
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        if len(nums) <= 3:
            return []
        nums.sort()
        result = set()
        for indx, val in enumerate(nums[:-3]):
            for secIndx in xrange(indx + 1, len(nums) - 2):  # at this point, becomes 2sum problem
                dic = {}  # need to find 2sum goal = target -val - nums[secIndx]
                for innerIndx in xrange(secIndx+1, len(nums)):
                    if nums[innerIndx] not in dic:
                        dic[target -val - nums[secIndx] - nums[innerIndx]] = 1
                    else:
                        result.add((target -val - nums[secIndx] - nums[innerIndx], val, nums[secIndx], nums[innerIndx]))
        return map(list, result)
```
