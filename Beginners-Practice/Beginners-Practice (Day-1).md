# 1. Two Sum
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]
Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]

```python
class Solution:
    def twoSum(self, nums, target):
        hashmap = {}
        for i, num in enumerate(nums):
            diff = target - num
            if diff in hashmap:
                return [hashmap[diff], i]
            hashmap[num] = i

# Example usage:
sol = Solution()
result = sol.twoSum([2, 7, 11, 15], 9)
print(result)

```

    [0, 1]
    

# 2.Palindrome Number
Given an integer x, return true if x is a palindrome, and false otherwise.

 

Example 1:

Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.
Example 2:

Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
 

Constraints:

-231 <= x <= 231 - 1

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        # Negative numbers are not palindrome
        if x < 0:
            return False
        # Convert number to string and compare with its reverse
        return str(x) == str(x)[::-1]

# Sample usage
sol = Solution()

# Test cases
print(sol.isPalindrome(121))    # Output: True
print(sol.isPalindrome(-121))   # Output: False
print(sol.isPalindrome(10))     # Output: False

```

    True
    False
    False
    

# 3. Roman to interger
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, 2 is written as II in Roman numeral, just two ones added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer.

 

Example 1:

Input: s = "III"
Output: 3
Explanation: III = 3.
Example 2:

Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
Example 3:

Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
 

Constraints:

1 <= s.length <= 15
s contains only the characters ('I', 'V', 'X', 'L', 'C', 'D', 'M').
It is guaranteed that s is a valid roman numeral in the range [1, 3999].

```python
# Your class definition
class Solution:
    def romanToInt(self, s: str) -> int:
        roman = {
            'I': 1,
            'V': 5,
            'X': 10,
            'L': 50,
            'C': 100,
            'D': 500,
            'M': 1000
        }
        
        total = 0
        prev_value = 0

        for ch in reversed(s):  # Iterate from right to left
            value = roman[ch]
            if value < prev_value:
                total -= value
            else:
                total += value
                prev_value = value

        return total

# Create an object and call the method
solution = Solution()
print(solution.romanToInt("MCMXCIV"))  # Example: "MCMXCIV" = 1994

```

    1994
    

# 4.Logest Common Prefix
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

 

Example 1:

Input: strs = ["flower","flow","flight"]
Output: "fl"
Example 2:

Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
 

Constraints:

1 <= strs.length <= 200
0 <= strs[i].length <= 200
strs[i] consists of only lowercase English letters if it is non-empty.

```python
class Solution:
    def longestCommonPrefix(self, strs: list[str]) -> str:
        if not strs:
            return ""

        # Start with the first string as the prefix
        prefix = strs[0]

        for word in strs[1:]:
            while not word.startswith(prefix):
                prefix = prefix[:-1]
                if prefix == "":
                    return ""

        return prefix

# Example usage
solution = Solution()
print(solution.longestCommonPrefix(["flower", "flow", "flight"]))  # Output: "fl"

```

    fl
    

# 5.Vaild Parenthese
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
 

Example 1:

Input: s = "()"

Output: true

Example 2:

Input: s = "()[]{}"

Output: true

Example 3:

Input: s = "(]"

Output: false

Example 4:

Input: s = "([])"

Output: true

 

Constraints:

1 <= s.length <= 104
s consists of parentheses only '()[]{}'.

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        bracket_map = {')': '(', '}': '{', ']': '['}

        for char in s:
            if char in bracket_map.values():  # If it's an opening bracket
                stack.append(char)
            elif char in bracket_map:  # If it's a closing bracket
                if not stack or stack[-1] != bracket_map[char]:
                    return False
                stack.pop()
            else:
                return False  # Invalid character (not needed for this problem)

        return len(stack) == 0

# Example test cases
solution = Solution()
print(solution.isValid("()"))        # Output: True
print(solution.isValid("()[]{}"))    # Output: True
print(solution.isValid("(]"))        # Output: False
print(solution.isValid("([])"))      # Output: True

```

    True
    True
    False
    True
    


```python

```
