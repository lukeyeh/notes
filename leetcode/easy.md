# Leetcode Easy Set Solutions

All problems solved by me. Should be all optimal, if not [PRs](https://www.github.com/lukeyeh/notes) are welcome.

## Array

### Remove Duplicates from Sorted Array

{% tabs %}
{% tab title="Problem" %}
Given a sorted array _nums_, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only _once_ and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array** [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.

**Example 1:**

```text
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```text
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```text
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```
{% endtab %}

{% tab title="Solution" %}
```python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        [0,0,1,1,1,2,2,3,3,4]
        j = 1
        i = 0
        for j in range(1, len(nums)):
            if nums[i] != nums[j]:
                i+=1
                nums[i] = nums[j]
        
        return i+1
```
{% endtab %}
{% endtabs %}

### Best Time to Buy and Sell Stock II Solution

{% tabs %}
{% tab title="Problem" %}
Say you have an array `prices` for which the _i_th element is the price of a given stock on day _i_.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like \(i.e., buy one and sell one share of the stock multiple times\).

**Note:** You may not engage in multiple transactions at the same time \(i.e., you must sell the stock before you buy again\).

**Example 1:**

```text
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

**Example 2:**

```text
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

**Example 3:**

```text
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

**Constraints:**

* `1 <= prices.length <= 3 * 10 ^ 4`
* `0 <= prices[i] <= 10 ^ 4`
{% endtab %}

{% tab title="Solution" %}
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        max_profit = 0
        for i in range(1, len(prices)):
            if prices[i] > prices[i-1]:
                max_profit+=prices[i]-prices[i-1]
        
        return max_profit
```
{% endtab %}
{% endtabs %}

### Rotate Array

{% tabs %}
{% tab title="Problem" %}
Given an array, rotate the array to the right by _k_ steps, where _k_ is non-negative.

**Follow up:**

* Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
* Could you do it in-place with O\(1\) extra space?

**Example 1:**

```text
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

**Example 2:**

```text
Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

**Constraints:**

* `1 <= nums.length <= 2 * 10^4`
* It's guaranteed that `nums[i]` fits in a 32 bit-signed integer.
* `k >= 0`
{% endtab %}

{% tab title="Solution" %}
```python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        new_idx = {}
        for i, num in enumerate(nums):
            new_idx[(i+k)%len(nums)] = num
        for i in range(len(nums)):
            nums[i] = new_idx[i]
```
{% endtab %}
{% endtabs %}

### Contains Duplicate

{% tabs %}
{% tab title="First Tab" %}
Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

**Example 1:**

```text
Input: [1,2,3,1]
Output: true
```

**Example 2:**

```text
Input: [1,2,3,4]
Output: false
```

**Example 3:**

```text
Input: [1,1,1,3,3,4,3,2,4,2]
Output: true
```
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        
        return False
```
{% endtab %}
{% endtabs %}

### Single Number

{% tabs %}
{% tab title="First Tab" %}
Given a **non-empty** array of integers, every element appears _twice_ except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**

```text
Input: [2,2,1]
Output: 1
```

**Example 2:**

```text
Input: [4,1,2,1,2]
Output: 4
```
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        counts = {}
        for num in nums:
            if not num in counts:
                counts[num] = 1
            else:
                counts[num]+=1
        
        for num in nums:
            if counts[num] == 1:
                return num
```
{% endtab %}
{% endtabs %}

### Intersection of Two Arrays II

{% tabs %}
{% tab title="First Tab" %}
Given two arrays, write a function to compute their intersection.

**Example 1:**

```text
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

**Example 2:**

```text
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
```

**Note:**

* Each element in the result should appear as many times as it shows in both arrays.
* The result can be in any order.

**Follow up:**

* What if the given array is already sorted? How would you optimize your algorithm?
* What if nums1's size is small compared to nums2's size? Which algorithm is better?
* What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution(object):
    def intersect(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        if len(nums1) > len(nums2):
            smaller = nums2
            bigger = nums1
        else:
            smaller = nums1
            bigger = nums2
        
        i_small, i_big = 0, 0
        intersection = []
        while i_small < len(smaller):
            i_big = 0
            matched = False
            while i_big < len(bigger) and i_small < len(smaller):
                if smaller[i_small] != bigger[i_big]:
                    i_big+=1
                else:
                    bigger[i_big] = float("inf")
                    intersection.append(smaller[i_small])
                    i_big+=1
                    i_small+=1 

                    matched = True
            if not matched: i_small+=1
        
        return intersection
```
{% endtab %}
{% endtabs %}

### Plus One

{% tabs %}
{% tab title="First Tab" %}
Given a **non-empty** array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

**Example 1:**

```text
Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

**Example 2:**

```text
Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        zeros = 10**(len(digits)-1)
        num_in_ints = 0
        for d in digits:
            num_in_ints+=(d*zeros)
            zeros/=10
        
        def num_length(num):
            length = 0
            while num != 0:
                length+=1
                num/=10
            return length
        
        num_in_ints+=1
        ans = [0 for i in range(num_length(num_in_ints))]
        i = len(ans)-1
        while i >= 0:
            ans[i] = num_in_ints%10
            num_in_ints/=10
            i-=1

                    
        return ans
```
{% endtab %}
{% endtabs %}

### Move Zeroes

{% tabs %}
{% tab title="First Tab" %}
Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```text
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note**:

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations.
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        idx_to_num = {}
        i, j = 0, len(nums)-1
        new_idx = 0
        while i < len(nums):
            if nums[i] != 0:
                idx_to_num[new_idx] = nums[i] 
                new_idx+=1
            else:
                idx_to_num[j] = nums[i]
                j-=1
            i+=1 
            
        for i, _ in enumerate(nums):
            nums[i] = idx_to_num[i]  
```
{% endtab %}
{% endtabs %}

### Two Sum

{% tabs %}
{% tab title="First Tab" %}
Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have _**exactly**_ one solution, and you may not use the _same_ element twice.

**Example:**

```text
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        
        compliments = {}
        for i, num in enumerate(nums): 
            if target - num in compliments:
                return compliments[target-num], i
            else:
                compliments[num] = i
            
```
{% endtab %}
{% endtabs %}

### Valid Sudoku

{% tabs %}
{% tab title="First Tab" %}
Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the 9 `3x3` sub-boxes of the grid must contain the digits `1-9` without repetition.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)  
A partially filled sudoku which is valid.

The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.
{% endtab %}

{% tab title="Second Tab" %}
```python
from collections import defaultdict

class Solution(object):
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        def which_subsquare(i, j):
            n, m = -1, -1
            def which_range(x): 
                if x >= 0 and x <= 2:
                    return 0
                elif x >= 3 and x <= 5:
                    return 1
                elif x >= 6 and x <= 8:
                    return 2
                else:
                    return -1
            n = which_range(i)
            m = which_range(j)
            
            return str(n) + str(m)
        
            
            
        mem = {i : {}  for i in ['row', 'column', 'square']} 
        
        
        for i in range(len(board)):
            for j in range(len(board[i])):
                if not i in mem['row']:
                    mem['row'][i] = set()
                if not j in mem['column']:
                    mem['column'][j] = set()
                k = which_subsquare(i,j)
                if not k in mem['square']:
                    mem['square'][k] = set()
                
                
                if board[i][j] != '.':
                    if board[i][j] in mem['row'][i]:
                        print(board[i][j])
                        print(mem)
                        return False
                    else:
                        mem['row'][i].add(board[i][j])

                    if board[i][j] in mem['column'][j]:
                        print(mem)
                        return False
                    else:
                        mem['column'][j].add(board[i][j])

                    if board[i][j] in mem['square'][k]:
                        print(board[i][j], i, j)

                        print(mem)
                        return False
                    else:
                        mem['square'][k].add(board[i][j])
        
        return True
```
{% endtab %}
{% endtabs %}

### Rotate Image

{% tabs %}
{% tab title="First Tab" %}
You are given an _n_ x _n_ 2D matrix representing an image.

Rotate the image by 90 degrees \(clockwise\).

**Note:**

You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

**Example 1:**

```text
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

**Example 2:**

```text
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: None Do not return anything, modify matrix in-place instead.
        """ 
        N = len(matrix)
        for i in range(N//2):
            for j in range(N-1-i): 
                temp = matrix[i][j]
                matrix[i][j] = matrix[N-1-i][j]
                matrix[N-1-i] = matrix[N-1-i][N-1-i] 
                matrix[N-1-i][N-1-i] = matrix[i][N-1-j]
                matrix[i][N-1-j] = temp
```
{% endtab %}
{% endtabs %}

## Strings

### Reverse String

{% tabs %}
{% tab title="First Tab" %}
Write a function that reverses a string. The input string is given as an array of characters `char[]`.

Do not allocate extra space for another array, you must do this by **modifying the input array** [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.

You may assume all the characters consist of [printable ascii characters](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

**Example 1:**

```text
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

**Example 2:**

```text
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution(object):
    def reverseString(self, s):
        """
        :type s: List[str]
        :rtype: None Do not return anything, modify s in-place instead.
        """
        i, j = 0, len(s)-1
        
        while i <= j:
            temp = s[i]
            s[i] = s[j]
            s[j] = temp
            i+=1
            j-=1
```
{% endtab %}
{% endtabs %}

### Reverse Integer

{% tabs %}
{% tab title="First Tab" %}
Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

```text
Input: 123
Output: 321
```

**Example 2:**

```text
Input: -123
Output: -321
```

**Example 3:**

```text
Input: 120
Output: 21
```

**Note:**  
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: \[−231,  231 − 1\]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.
{% endtab %}

{% tab title="Second Tab" %}
```python
import sys
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        
        neg = x < 0
        x = abs(x) 
            
        def len_num(num):
            length = 0
            while num > 0: 
                num/=10
                length+=1
                
            return length
        
        ans = 0
        u = len_num(x)-1
        while x != 0:
            last = x%10 
            ans += last*(10**u)
            x/=10
            u-=1
            
            
        if ans < -1 * 2**31 or ans > 2**31-1: return 0

        
        return -1 * ans if neg else ans
```
{% endtab %}
{% endtabs %}

### First Unique Character in a String

{% tabs %}
{% tab title="First Tab" %}
Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**

```text
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```

**Note:** You may assume the string contain only lowercase English letters.
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        mem = {} 
        
        for i, l in enumerate(s): 
            if l not in mem: 
                mem[l] = set()
            mem[l].add(i)
                    
        for l in s:
            if len(mem[l]) == 1:
                return list(mem[l])[0]
        
        return -1
```
{% endtab %}
{% endtabs %}

### Valid Anagram

{% tabs %}
{% tab title="First Tab" %}
Given two strings _s_ and _t_ , write a function to determine if _t_ is an anagram of _s_.

**Example 1:**

```text
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```text
Input: s = "rat", t = "car"
Output: false
```

**Note:**  
You may assume the string contains only lowercase alphabets.

**Follow up:**  
What if the inputs contain unicode characters? How would you adapt your solution to such case?
{% endtab %}

{% tab title="Second Tab" %}
```python
from collections import Counter
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(t)
```
{% endtab %}
{% endtabs %}

### Valid Palindrome

{% tabs %}
{% tab title="First Tab" %}
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Note:** For the purpose of this problem, we define empty string as valid palindrome.

**Example 1:**

```text
Input: "A man, a plan, a canal: Panama"
Output: true
```

**Example 2:**

```text
Input: "race a car"
Output: false
```
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = list(filter(lambda x : x.isalnum(), list(s.lower())))
        i, j = 0, len(s)-1
        while i <= j: 
            if s[i] != s[j]:
                return False
            i+=1
            j-=1
        return True
```
{% endtab %}
{% endtabs %}

### Implement strStr\(\)

{% tabs %}
{% tab title="First Tab" %}
Implement [strStr\(\)](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

**Example 1:**

```text
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```text
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

**Clarification:**

What should we return when `needle` is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr\(\)](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf\(\)](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf%28java.lang.String%29).
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        i, j = 0, len(needle)-1
        while j < len(haystack):
            if haystack[i:j+1] == needle:
                return i
            i, j = i+1, j+1
        return -1
```
{% endtab %}
{% endtabs %}

### Count and Say

{% tabs %}
{% tab title="First Tab" %}
The count-and-say sequence is the sequence of integers with the first five terms as following:

```text
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

`1` is read off as `"one 1"` or `11`.  
`11` is read off as `"two 1s"` or `21`.  
`21` is read off as `"one 2`, then `one 1"` or `1211`.

Given an integer n where 1 ≤ _n_ ≤ 30, generate the nth term of the count-and-say sequence. You can do so recursively, in other words from the previous member read off the digits, counting the number of digits in groups of the same digit.

Note: Each term of the sequence of integers will be represented as a string.

**Example 1:**

```text
Input: 1
Output: "1"
Explanation: This is the base case.
```

**Example 2:**

```text
Input: 4
Output: "1211"
Explanation: For n = 3 the term was "21" in which we have two groups "2" and "1", "2" can be read as "12" which means frequency = 1 and value = 2, the same way "1" is read as "11", so the answer is the concatenation of "12" and "11" which is "1211".
```
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution:    
    def getNext(self, s: str) -> str:
        i, j = 0, 0
        ans = ""
        curr_count = 0
        while i < len(s) and j < len(s):
            if s[i] != s[j]:
                ans = ans + str(curr_count) + s[j-1]
                curr_count=0
                i=j
            else:
                curr_count+=1
                j+=1
        
        ans = ans + str(curr_count) + s[j-1]
        return ans

    def countAndSay(self, n: int) -> str:
        
        if n == 1:
            return "1"
        
        prev = self.countAndSay(n-1)
        ans = self.getNext(prev)
        
        return ans
```
{% endtab %}
{% endtabs %}

### Longest Common Prefix

{% tabs %}
{% tab title="First Tab" %}
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```text
Input: ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```text
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

**Note:**

All given inputs are in lowercase letters `a-z`.
{% endtab %}

{% tab title="Second Tab" %}
```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if len(strs) == 0: return ""

        i, j = 0, 0
        
        min_len = min(map(lambda x: len(x), strs))
        max_length = -1
        max_range = (-1, -1)
        
        while j < min_len:
            prev = strs[0]
            range_valid = True
            
            for s in strs:
                if prev[i:j+1] != s[i:j+1]:
                    range_valid = False
                prev = s
                    
            if range_valid: 
                if j-i > max_length:
                    max_range = (i, j)
                    max_length = j-i
                    
            j+=1

        if max_length == -1: return ""
        return strs[0][max_range[0]:max_range[1]+1]
```
{% endtab %}
{% endtabs %}

## LinkedLists

### Delete Node in a Linked List

### Remove Nth Node From End of List

### Reverse Linked List

### Merge Two Sorted Lists

### Palindrome Linked List

### Linked List Cycle

## Trees

### Maximum Depth of Binary Tree

### Validate Binary Search Tree

### Symmetric Tree

### Binary Tree Level Order Traversal

### Convert Sorted Array to Binary Search Tree

{% tabs %}
{% tab title="Problem" %}
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of _every_ node never differ by more than 1.

**Example:**

```text
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
 
```
{% endtab %}

{% tab title="Solution" %}
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> TreeNode:
        if len(nums) == 0:
            return None
        if len(nums) == 1:
            return TreeNode(val=nums[0])
        mid = len(nums)//2
        left = self.sortedArrayToBST(nums[:mid])
        right = self.sortedArrayToBST(nums[mid+1:])
        print(nums[mid], nums)
        root = TreeNode(val=nums[mid], left=left, right=right)
        return root
    
```
{% endtab %}
{% endtabs %}

### Binary Tree Level Order Traversal

{% tabs %}
{% tab title="Problem" %}
Given a binary tree, return the level order traversal of its nodes' values. \(ie, from left to right, level by level\).

For example:  
Given binary tree `[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```text
[
  [3],
  [9,20],
  [15,7]
]
```
{% endtab %}

{% tab title="Solution" %}
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def helper(self, root: TreeNode, ans)
        if root is None:
            return
        
        level_ans = []
        level_ans.append(root.left.val, root.right.val)
        ans.append(level_ans)
        self.helper(root.left, ans)
        self.helper(root.right, ans)
        
        return ans
    
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        return self.helper(root, [])
```
{% endtab %}
{% endtabs %}

### Symmetric Trees

Given a binary tree, check whether it is a mirror of itself \(ie, symmetric around its center\).

{% tabs %}
{% tab title="Problem" %}
Given a binary tree, check whether it is a mirror of itself \(ie, symmetric around its center\).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```text
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following `[1,2,2,null,3,null,3]` is not:

```text
    1
   / \
  2   2
   \   \
   3    3
```

**Follow up:** Solve it both recursively and iteratively.
{% endtab %}

{% tab title="Solution" %}
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def helper(self, root_left, root_right):
        if root_left is None and root_right is None:
            return True
        if root_left is None or root_right is None:
            return False
        
        level = root_left.val == root_right.val
        left = self.helper(root_left.left, root_right.right)
        right = self.helper(root_left.right, root_right.left)
        return level and left and right
    
    def isSymmetric(self, root):
        return self.helper(root, root)
```
{% endtab %}
{% endtabs %}

**Follow up:** Solve it both recursively and iteratively.

## Sort and Searching

### Merge Sorted Array

{% tabs %}
{% tab title="Problem" %}
Given two sorted integer arrays _nums1_ and _nums2_, merge _nums2_ into _nums1_ as one sorted array.

**Note:**

* The number of elements initialized in _nums1_ and _nums2_ are _m_ and _n_ respectively.
* You may assume that _nums1_ has enough space \(size that is greater or equal to _m_ + _n_\) to hold additional elements from _nums2_.

**Example:**

```text
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```
{% endtab %}

{% tab title="Solution" %}
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        i1 = m-1
        i2 = n-1
        write_idx = len(nums1)-1
        
        while write_idx >= 0 and i2 >= 0:
            if nums1[i1] < nums2[i2] or i1 < 0:
                nums1[write_idx] = nums2[i2]
                i2-=1
            else:
                nums1[write_idx] = nums1[i1]
                i1-=1
            write_idx-=1     
```
{% endtab %}
{% endtabs %}

### First Bad Version

{% tabs %}
{% tab title="Problem" %}
You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which will return whether `version` is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

**Example:**

```text
Given n = 5, and version = 4 is the first bad version.

call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true

Then 4 is the first bad version. 
```
{% endtab %}

{% tab title="Solution" %}
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        i1 = m-1
        i2 = n-1
        write_idx = len(nums1)-1
        
        while write_idx >= 0 and i2 >= 0:
            if nums1[i1] < nums2[i2] or i1 < 0:
                nums1[write_idx] = nums2[i2]
                i2-=1
            else:
                nums1[write_idx] = nums1[i1]
                i1-=1
            write_idx-=1
```
{% endtab %}
{% endtabs %}

