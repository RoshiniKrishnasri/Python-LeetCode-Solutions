# 1.longest palindromic substring
Given a string s, return the longest palindromic substring in s.

 

Example 1:

Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
Example 2:

Input: s = "cbbd"
Output: "bb"
 

Constraints:

1 <= s.length <= 1000
s consist of only digits and English letters.

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if not s or len(s) < 1:
            return ""

        start, end = 0, 0

        for i in range(len(s)):
            len1 = self.expand_from_center(s, i, i)      # Odd length
            len2 = self.expand_from_center(s, i, i + 1)  # Even length
            max_len = max(len1, len2)

            if max_len > (end - start):
                start = i - (max_len - 1) // 2
                end = i + max_len // 2

        return s[start:end + 1]

    def expand_from_center(self, s: str, left: int, right: int) -> int:
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return right - left - 1

# Example usage
print(Solution().longestPalindrome("babad"))  # Output: "bab" or "aba"
print(Solution().longestPalindrome("cbbd"))   # Output: "bb"

```

    aba
    bb
    

# 2. Container with Most Water
You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

 

Example 1:


Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
Example 2:

Input: height = [1,1]
Output: 1
 

Constraints:

n == height.length
2 <= n <= 105
0 <= height[i] <= 104

```python
class Solution:
    def maxArea(self, height):
        left = 0
        right = len(height) - 1
        max_area = 0

        while left < right:
            width = right - left
            ht = min(height[left], height[right])
            area = width * ht
            print(f"Left: {left}, Right: {right}, "
                  f"Height[left]: {height[left]}, Height[right]: {height[right]}, "
                  f"Width: {width}, Height: {ht}, Area: {area}")
            
            max_area = max(max_area, area)
            print(f"Updated Max Area: {max_area}\n")

            if height[left] < height[right]:
                left += 1
            else:
                right -= 1

        return max_area

# Example usage
heights = [1, 8, 6, 2, 5, 4, 8, 3, 7]
sol = Solution()
result = sol.maxArea(heights)
print(" Final Maximum Area:", result)

```

    Left: 0, Right: 8, Height[left]: 1, Height[right]: 7, Width: 8, Height: 1, Area: 8
    Updated Max Area: 8
    
    Left: 1, Right: 8, Height[left]: 8, Height[right]: 7, Width: 7, Height: 7, Area: 49
    Updated Max Area: 49
    
    Left: 1, Right: 7, Height[left]: 8, Height[right]: 3, Width: 6, Height: 3, Area: 18
    Updated Max Area: 49
    
    Left: 1, Right: 6, Height[left]: 8, Height[right]: 8, Width: 5, Height: 8, Area: 40
    Updated Max Area: 49
    
    Left: 1, Right: 5, Height[left]: 8, Height[right]: 4, Width: 4, Height: 4, Area: 16
    Updated Max Area: 49
    
    Left: 1, Right: 4, Height[left]: 8, Height[right]: 5, Width: 3, Height: 5, Area: 15
    Updated Max Area: 49
    
    Left: 1, Right: 3, Height[left]: 8, Height[right]: 2, Width: 2, Height: 2, Area: 4
    Updated Max Area: 49
    
    Left: 1, Right: 2, Height[left]: 8, Height[right]: 6, Width: 1, Height: 6, Area: 6
    Updated Max Area: 49
    
     Final Maximum Area: 49
    

# 3.Zigzag Conversion
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P   A   H   N
A P L S I I G
Y   I   R
And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:

string convert(string s, int numRows);
 

Example 1:

Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
Example 2:

Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:
P     I    N
A   L S  I G
Y A   H R
P     I
Example 3:

Input: s = "A", numRows = 1
Output: "A"
 

Constraints:

1 <= s.length <= 1000
s consists of English letters (lower-case and upper-case), ',' and '.'.
1 <= numRows <= 1000

```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        # Special case: if numRows is 1, the zigzag is just a straight line
        if numRows == 1 or numRows >= len(s):
            return s

        # Create a list to store strings for each row
        rows = ['' for _ in range(numRows)]
        curr_row = 0
        going_down = False

        # Iterate through each character and place it in the correct row
        for char in s:
            print(f"Character '{char}' goes to row {curr_row}")
            rows[curr_row] += char

            # Change direction at the top or bottom row
            if curr_row == 0 or curr_row == numRows - 1:
                going_down = not going_down
            
            # Move up or down
            curr_row += 1 if going_down else -1

        # Display the rows after placement
        print("\nRows after zigzag placement:")
        for i, row in enumerate(rows):
            print(f"Row {i}: {row}")

        # Concatenate rows to get the final zigzag string
        result = ''.join(rows)
        print("\nFinal Zigzag String:", result)
        return result

# Example usage
s = "PAYPALISHIRING"
numRows = 4
sol = Solution()
sol.convert(s, numRows)

```

    Character 'P' goes to row 0
    Character 'A' goes to row 1
    Character 'Y' goes to row 2
    Character 'P' goes to row 3
    Character 'A' goes to row 2
    Character 'L' goes to row 1
    Character 'I' goes to row 0
    Character 'S' goes to row 1
    Character 'H' goes to row 2
    Character 'I' goes to row 3
    Character 'R' goes to row 2
    Character 'I' goes to row 1
    Character 'N' goes to row 0
    Character 'G' goes to row 1
    
    Rows after zigzag placement:
    Row 0: PIN
    Row 1: ALSIG
    Row 2: YAHR
    Row 3: PI
    
    Final Zigzag String: PINALSIGYAHRPI
    




    'PINALSIGYAHRPI'



# 4. integer to Roman 
Seven different symbols represent Roman numerals with the following values:

Symbol	Value
I	1
V	5
X	10
L	50
C	100
D	500
M	1000
Roman numerals are formed by appending the conversions of decimal place values from highest to lowest. Converting a decimal place value into a Roman numeral has the following rules:

If the value does not start with 4 or 9, select the symbol of the maximal value that can be subtracted from the input, append that symbol to the result, subtract its value, and convert the remainder to a Roman numeral.
If the value starts with 4 or 9 use the subtractive form representing one symbol subtracted from the following symbol, for example, 4 is 1 (I) less than 5 (V): IV and 9 is 1 (I) less than 10 (X): IX. Only the following subtractive forms are used: 4 (IV), 9 (IX), 40 (XL), 90 (XC), 400 (CD) and 900 (CM).
Only powers of 10 (I, X, C, M) can be appended consecutively at most 3 times to represent multiples of 10. You cannot append 5 (V), 50 (L), or 500 (D) multiple times. If you need to append a symbol 4 times use the subtractive form.
Given an integer, convert it to a Roman numeral.

 

Example 1:

Input: num = 3749

Output: "MMMDCCXLIX"

Explanation:

3000 = MMM as 1000 (M) + 1000 (M) + 1000 (M)
 700 = DCC as 500 (D) + 100 (C) + 100 (C)
  40 = XL as 10 (X) less of 50 (L)
   9 = IX as 1 (I) less of 10 (X)
Note: 49 is not 1 (I) less of 50 (L) because the conversion is based on decimal places
Example 2:

Input: num = 58

Output: "LVIII"

Explanation:

50 = L
 8 = VIII
Example 3:

Input: num = 1994

Output: "MCMXCIV"

Explanation:

1000 = M
 900 = CM
  90 = XC
   4 = IV
    Constraints:

1 <= num <= 3999

```python
class Solution:
    def intToRoman(self, num):
        val_map = [
            (1000, 'M'),
            (900, 'CM'),
            (500, 'D'),
            (400, 'CD'),
            (100, 'C'),
            (90, 'XC'),
            (50, 'L'),
            (40, 'XL'),
            (10, 'X'),
            (9, 'IX'),
            (5, 'V'),
            (4, 'IV'),
            (1, 'I')
        ]

        roman = []
        print(f"\n Converting number: {num}")
        for value, symbol in val_map:
            count = 0
            while num >= value:
                roman.append(symbol)
                num -= value
                count += 1
            if count > 0:
                print(f" Appended '{symbol}' x {count} → Remaining number: {num}")

        result = ''.join(roman)
        print(" Final Roman numeral:", result)
        return result


# Example Usage with Output

sol = Solution()

# Example 1: 3 → "III"
print("\n Example 1: num = 3")
sol.intToRoman(3)

# Example 2: 58 → "LVIII"
print("\n Example 2: num = 58")
sol.intToRoman(58)

# Example 3: 1994 → "MCMXCIV"
print("\n Example 3: num = 1994")
sol.intToRoman(1994)

```

    
     Example 1: num = 3
    
     Converting number: 3
     Appended 'I' x 3 → Remaining number: 0
     Final Roman numeral: III
    
     Example 2: num = 58
    
     Converting number: 58
     Appended 'L' x 1 → Remaining number: 8
     Appended 'V' x 1 → Remaining number: 3
     Appended 'I' x 3 → Remaining number: 0
     Final Roman numeral: LVIII
    
     Example 3: num = 1994
    
     Converting number: 1994
     Appended 'M' x 1 → Remaining number: 994
     Appended 'CM' x 1 → Remaining number: 94
     Appended 'XC' x 1 → Remaining number: 4
     Appended 'IV' x 1 → Remaining number: 0
     Final Roman numeral: MCMXCIV
    




    'MCMXCIV'



# 5.3Sumclosest
Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.

Return the sum of the three integers.

You may assume that each input would have exactly one solution.

 

Example 1:

Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
Example 2:

Input: nums = [0,0,0], target = 1
Output: 0
Explanation: The sum that is closest to the target is 0. (0 + 0 + 0 = 0).
 

Constraints:

3 <= nums.length <= 500
-1000 <= nums[i] <= 1000
-104 <= target <= 104

```python
class Solution:
    def threeSumClosest(self, nums, target):
        nums.sort()
        print(f"\nSorted nums: {nums}")
        closest_sum = float('inf')
        n = len(nums)

        for i in range(n - 2):
            left = i + 1
            right = n - 1

            print(f"\nBase index i = {i}, value = {nums[i]}")

            while left < right:
                total = nums[i] + nums[left] + nums[right]
                print(f"  Trying triplet: {nums[i]}, {nums[left]}, {nums[right]} → total = {total}")

                if abs(target - total) < abs(target - closest_sum):
                    closest_sum = total
                    print(f"  Updated closest_sum to {closest_sum}")

                if total < target:
                    print(f"  total < target → Moving left pointer from {left} to {left + 1}")
                    left += 1
                elif total > target:
                    print(f"  total > target → Moving right pointer from {right} to {right - 1}")
                    right -= 1
                else:
                    print(f"  Exact match found with total = {total}")
                    return total

        print(f"\nClosest sum to target {target} is: {closest_sum}")
        return closest_sum

# Example input
sol = Solution()
nums = [-1, 2, 1, -4]
target = 1

print("\nExample Input:")
result = sol.threeSumClosest(nums, target)
print("\nFinal Result:", result)

```

    
    Example Input:
    
    Sorted nums: [-4, -1, 1, 2]
    
    Base index i = 0, value = -4
      Trying triplet: -4, -1, 2 → total = -3
      Updated closest_sum to -3
      total < target → Moving left pointer from 1 to 2
      Trying triplet: -4, 1, 2 → total = -1
      Updated closest_sum to -1
      total < target → Moving left pointer from 2 to 3
    
    Base index i = 1, value = -1
      Trying triplet: -1, 1, 2 → total = 2
      Updated closest_sum to 2
      total > target → Moving right pointer from 3 to 2
    
    Closest sum to target 1 is: 2
    
    Final Result: 2
    


```python

```
