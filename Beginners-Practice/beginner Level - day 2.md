# 1.search to positon
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

 

Example 1:

Input: nums = [1,3,5,6], target = 5
Output: 2
Example 2:

Input: nums = [1,3,5,6], target = 2
Output: 1
Example 3:

Input: nums = [1,3,5,6], target = 7
Output: 4
 

Constraints:

1 <= nums.length <= 104

```python
class Solution:
    def searchInsert(self, nums, target):
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1

        return left


sol = Solution()

# Run Examples
print(sol.searchInsert([1, 3, 5, 6], 5))  
print(sol.searchInsert([1, 3, 5, 6], 2))  
print(sol.searchInsert([1, 3, 5, 6], 7))  
print(sol.searchInsert([1, 3, 5, 6], 0)) 

```

    2
    1
    4
    0
    

# 2.Plus One
You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

 

Example 1:

Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].
Example 2:

Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].
Example 3:

Input: digits = [9]
Output: [1,0]
Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].
 

Constraints:

1 <= digits.length <= 100
0 <= digits[i] <= 9
digits does not contain any leading 0's.


```python
class Solution:
    def plusOne(self, digits):
        n = len(digits)

        for i in range(n - 1, -1, -1):
            if digits[i] < 9:
                digits[i] += 1
                return digits
            digits[i] = 0  # carry over

        return [1] + digits  # all digits were 9


# Create an instance of the class
sol = Solution()

# Test cases
examples = [
    [1, 2, 3],     
    [4, 3, 2, 1],  
    [9],            
    [9, 9, 9]       
]


for i, digits in enumerate(examples, 1):
    result = sol.plusOne(digits.copy())  
    print(f"Example {i}: Input = {digits} → Output = {result}")

```

    Example 1: Input = [1, 2, 3] → Output = [1, 2, 4]
    Example 2: Input = [4, 3, 2, 1] → Output = [4, 3, 2, 2]
    Example 3: Input = [9] → Output = [1, 0]
    Example 4: Input = [9, 9, 9] → Output = [1, 0, 0, 0]
    


```python

```
