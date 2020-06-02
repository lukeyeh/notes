---
description: All problems solved by me.
---

# Leetcode Easy Set Solutions

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

### Contains Duplicate

### Single Number

### Intersection of Two Arrays II

### Plus One

### Move Zeroes

### Two Sum

### Valid Sudoku

### Rotate Image

## Strings

### Reverse String

### Reverse Integer

### First Unique Character in a String

### Valid Anagram

### Valid Palindrome

### Implement strStr\(\)

### Count and Say

### Longest Common Prefix

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

