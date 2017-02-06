# Shuffle an Array

> Shuffle a set of numbers without duplicates.

> Example:

> ```
// Init an array with set 1, 2, and 3.
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// Shuffle the array [1,2,3] and return its result. Any permutation of [1,2,3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1,2,3].
solution.reset();

// Returns the random shuffling of array [1,2,3].
solution.shuffle();
```

The idea is to use two random seeds to represent the index of the value to be exchanged. After exchange the two randomly chosen value, the array is shuffled. It's wired that in the reset() method, if reset result back to original cannot be accepted by leetcode OJ. 

```Python
class Solution(object):

    def __init__(self, nums):
        """
        :type nums: List[int]
        """
        self.original = list(nums)
        self.result = list(nums)
        

    def reset(self):
        """
        Resets the array to its original configuration and return it.
        :rtype: List[int]
        """
        return self.original
        

    def shuffle(self):
        """
        Returns a random shuffling of the array.
        :rtype: List[int]
        """
        if len(self.result) == 0: return self.result
        import random
        rndSeed1 = random.randint(0, len(self.original)-1)
        rndSeed2 = random.randint(0, len(self.original)-1)
        tmp = self.result[rndSeed1]
        self.result[rndSeed1] = self.result[rndSeed2]
        self.result[rndSeed2] = tmp
        return self.result
        


# Your Solution object will be instantiated and called as such:
# obj = Solution(nums)
# param_1 = obj.reset()
# param_2 = obj.shuffle()
```
