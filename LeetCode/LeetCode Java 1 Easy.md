## 1. Two Sum

```embed
title: "Two Sum - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Two Sum - Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.  You may assume that each input would have exactly one solution, and you may not use the same element twice.  You can return the answer in any order.     Example 1:   Input: nums = [2,7,11,15], target = 9 Output: [0,1] Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].   Example 2:   Input: nums = [3,2,4], target = 6 Output: [1,2]   Example 3:   Input: nums = [3,3], target = 6 Output: [0,1]      Constraints:   * 2 <= nums.length <= 104  * -109 <= nums[i] <= 109  * -109 <= target <= 109  * Only one valid answer exists.     Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?"
url: "https://leetcode.com/problems/two-sum/description/"
favicon: ""
aspectRatio: "52"
```


```java
public class TwoSum {
    public static int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            int complement = target - num;
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }
          
	        map.put(num, i);
        }
        return new int[] {};
    }
}
```

## 9. Palindrome Number

```embed
title: "Palindrome Number - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Palindrome Number - Given an integer x, return true if x is a palindrome, and false otherwise.     Example 1:   Input: x = 121 Output: true Explanation: 121 reads as 121 from left to right and from right to left.   Example 2:   Input: x = -121 Output: false Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.   Example 3:   Input: x = 10 Output: false Explanation: Reads 01 from right to left. Therefore it is not a palindrome.      Constraints:   * -231 <= x <= 231 - 1     Follow up: Could you solve it without converting the integer to a string?"
url: "https://leetcode.com/problems/palindrome-number/"
favicon: ""
aspectRatio: "52"
```


```java
class Solution {
    public boolean isPalindrome(int x) {
        int rev = 0;
        int n = x;
        if (x < 0) {
            return false;
        }
        while (n != 0) {
            rev = rev * 10 + (n % 10);
            n = n / 10;
        }
        if (rev == x) {
            return true;
        } else {
            return false;
        }
    }
}
```

## 13. Roman to integer

```embed
title: "Roman to Integer - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Roman to Integer - Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.   Symbol       Value I             1 V             5 X             10 L             50 C             100 D             500 M             1000  For example, 2 is written as II in Roman numeral, just two ones added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.  Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:   * I can be placed before V (5) and X (10) to make 4 and 9.   * X can be placed before L (50) and C (100) to make 40 and 90.   * C can be placed before D (500) and M (1000) to make 400 and 900.  Given a roman numeral, convert it to an integer.     Example 1:   Input: s = \"III\" Output: 3 Explanation: III = 3.   Example 2:   Input: s = \"LVIII\" Output: 58 Explanation: L = 50, V= 5, III = 3.   Example 3:   Input: s = \"MCMXCIV\" Output: 1994 Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.      Constraints:   * 1 <= s.length <= 15  * s contains only the characters ('I', 'V', 'X', 'L', 'C', 'D', 'M').  * It is guaranteed that s is a valid roman numeral in the range [1, 3999]."
url: "https://leetcode.com/problems/roman-to-integer/"
favicon: ""
aspectRatio: "52"
```


```java
class Solution {
    public int romanToInt(String s) {
        HashMap<Character, Integer> map = new HashMap<>();
        map.put('I', 1);
        map.put('V', 5);
        map.put('X', 10);
        map.put('L', 50);
        map.put('C', 100);
        map.put('D', 500);
        map.put('M', 1000);
        int total = 0;
        for (int i = 0; i < s.length(); i++) {
            int value = map.get(s.charAt(i));
            if (i + 1 < s.length()) {
                int nextValue = map.get(s.charAt(i + 1));
                if (value < nextValue) {
                    total -= value;
                } else {
                    total += value;
                }
            } else {
                total += value;
            }
        }
        return total;
    }
}

```

## 14. Longest Common Prefix

```embed
title: "Longest Common Prefix - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Longest Common Prefix - Write a function to find the longest common prefix string amongst an array of strings.  If there is no common prefix, return an empty string \"\".     Example 1:   Input: strs = [\"flower\",\"flow\",\"flight\"] Output: \"fl\"   Example 2:   Input: strs = [\"dog\",\"racecar\",\"car\"] Output: \"\" Explanation: There is no common prefix among the input strings.      Constraints:   * 1 <= strs.length <= 200  * 0 <= strs[i].length <= 200  * strs[i] consists of only lowercase English letters if it is non-empty."
url: "https://leetcode.com/problems/longest-common-prefix/"
favicon: ""
aspectRatio: "52"
```


```cpp
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) return "";
        String prefix = strs[0];
        for (int i = 1; i < strs.length; i++) {
            while (strs[i].indexOf(prefix) != 0) {
                prefix = prefix.substring(0, prefix.length() - 1)
                if (prefix.isEmpty()) {
                    return "";
                }
            }
        }
        return prefix;
    }
}
```

## 20. Valid Parentheses

```embed
title: "Valid Parentheses - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Valid Parentheses - Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.  An input string is valid if:   1. Open brackets must be closed by the same type of brackets.  2. Open brackets must be closed in the correct order.  3. Every close bracket has a corresponding open bracket of the same type.     Example 1:  Input: s = \"()\"  Output: true  Example 2:  Input: s = \"()[]{}\"  Output: true  Example 3:  Input: s = \"(]\"  Output: false  Example 4:  Input: s = \"([])\"  Output: true  Example 5:  Input: s = \"([)]\"  Output: false     Constraints:   * 1 <= s.length <= 104  * s consists of parentheses only '()[]{}'."
url: "https://leetcode.com/problems/valid-parentheses/"
favicon: ""
aspectRatio: "52"
```


```cpp
class Solution {
    public boolean isValid(String s) {
        int l = s.length();
        Stack<Character> stack = new Stack<>();
        for (int i = 0; i < l; i++) {
            char c = s.charAt(i);
            
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            }
            else if (c == ')' || c == '}' || c == ']') {
                if (stack.isEmpty()) return false;
                char top = stack.peek();
                if ((c == ')' && top == '(') || 
                    (c == ']' && top == '[') || 
                    (c == '}' && top == '{')) {
                    stack.pop();
                } else {
                    return false;
                }
            }
        }
        
        return stack.isEmpty();
    }
}

```

## 21. Merge Two Sorted Lists

```embed
title: "Merge Two Sorted Lists - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Merge Two Sorted Lists - You are given the heads of two sorted linked lists list1 and list2.  Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.  Return the head of the merged linked list.     Example 1:  [https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg]   Input: list1 = [1,2,4], list2 = [1,3,4] Output: [1,1,2,3,4,4]   Example 2:   Input: list1 = [], list2 = [] Output: []   Example 3:   Input: list1 = [], list2 = [0] Output: [0]      Constraints:   * The number of nodes in both lists is in the range [0, 50].  * -100 <= Node.val <= 100  * Both list1 and list2 are sorted in non-decreasing order."
url: "https://leetcode.com/problems/merge-two-sorted-lists/"
favicon: ""
aspectRatio: "52"
```


```cpp
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
 
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(-1);
        ListNode curr = dummy;
        while (list1 != null && list2 != null) {
            if (list1.val <= list2.val) {
                curr.next = list1;
                list1 = list1.next;
            } else {
                curr.next = list2;
                list2 = list2.next;
            }
            curr = curr.next;
        }
        if (list1 != null) {
            curr.next = list1;
        } else {
            curr.next = list2;
        }
        return dummy.next;
    }
}

```

## 26.  Remove Duplicates from Sorted Array

```embed
title: "Remove Duplicates from Sorted Array - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Remove Duplicates from Sorted Array - Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place [https://en.wikipedia.org/wiki/In-place_algorithm] such that each unique element appears only once. The relative order of the elements should be kept the same.  Consider the number of unique elements in nums to be k . After removing duplicates, return the number of unique elements k.  The first k elements of nums should contain the unique numbers in sorted order. The remaining elements beyond index k - 1 can be ignored.  Custom Judge:  The judge will test your solution with the following code:   int[] nums = [...]; // Input array int[] expectedNums = [...]; // The expected answer with correct length  int k = removeDuplicates(nums); // Calls your implementation  assert k == expectedNums.length; for (int i = 0; i < k; i++) {     assert nums[i] == expectedNums[i]; }   If all assertions pass, then your solution will be accepted.     Example 1:   Input: nums = [1,1,2] Output: 2, nums = [1,2,_] Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively. It does not matter what you leave beyond the returned k (hence they are underscores).   Example 2:   Input: nums = [0,0,1,1,1,2,2,3,3,4] Output: 5, nums = [0,1,2,3,4,_,_,_,_,_] Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively. It does not matter what you leave beyond the returned k (hence they are underscores).      Constraints:   * 1 <= nums.length <= 3 * 104  * -100 <= nums[i] <= 100  * nums is sorted in non-decreasing order."
url: "https://leetcode.com/problems/remove-duplicates-from-sorted-array/"
favicon: ""
aspectRatio: "52"
```


```cpp

class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int i = 0;
        for (int j = 1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }
}

```

## 27. Remove Element

```embed
title: "Remove Element - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Remove Element - Given an integer array nums and an integer val, remove all occurrences of val in nums in-place [https://en.wikipedia.org/wiki/In-place_algorithm]. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.  Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:   * Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.  * Return k.  Custom Judge:  The judge will test your solution with the following code:   int[] nums = [...]; // Input array int val = ...; // Value to remove int[] expectedNums = [...]; // The expected answer with correct length.                             // It is sorted with no values equaling val.  int k = removeElement(nums, val); // Calls your implementation  assert k == expectedNums.length; sort(nums, 0, k); // Sort the first k elements of nums for (int i = 0; i < actualLength; i++) {     assert nums[i] == expectedNums[i]; }   If all assertions pass, then your solution will be accepted.     Example 1:   Input: nums = [3,2,2,3], val = 3 Output: 2, nums = [2,2,_,_] Explanation: Your function should return k = 2, with the first two elements of nums being 2. It does not matter what you leave beyond the returned k (hence they are underscores).   Example 2:   Input: nums = [0,1,2,2,3,0,4,2], val = 2 Output: 5, nums = [0,1,4,0,3,_,_,_] Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4. Note that the five elements can be returned in any order. It does not matter what you leave beyond the returned k (hence they are underscores).      Constraints:   * 0 <= nums.length <= 100  * 0 <= nums[i] <= 50  * 0 <= val <= 100"
url: "https://leetcode.com/problems/remove-element/"
favicon: ""
aspectRatio: "52"
```


```cpp
class Solution {
    public int removeElement(int[] nums, int val) {
        int k = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[k] = nums[i];
                k++;
            }
        }
        return k;
    }
}

```

## 28. Find the Index of the First Occurrence in a String

```embed
title: "Find the Index of the First Occurrence in a String - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Find the Index of the First Occurrence in a String - Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.     Example 1:   Input: haystack = \"sadbutsad\", needle = \"sad\" Output: 0 Explanation: \"sad\" occurs at index 0 and 6. The first occurrence is at index 0, so we return 0.   Example 2:   Input: haystack = \"leetcode\", needle = \"leeto\" Output: -1 Explanation: \"leeto\" did not occur in \"leetcode\", so we return -1.      Constraints:   * 1 <= haystack.length, needle.length <= 104  * haystack and needle consist of only lowercase English characters."
url: "https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/"
favicon: ""
aspectRatio: "52"
```


```cpp
class Solution {
    public int strStr(String haystack, String needle) {
        int nh = haystack.length();
        int nn = needle.length();
        if (nn == 0) return 0; // optional: LeetCode expects this
        for (int i = 0; i <= nh - nn; i++) {
            int j = 0;
            while (j < nn && haystack.charAt(i + j) == needle.charAt(j)) {
                j++;
            }
            if (j == nn) {
                return i;
            }
        }
        return -1;
    }
}

```

## 35. Search Insert Position

```embed
title: "Search Insert Position - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Search Insert Position - Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.  You must write an algorithm with O(log n) runtime complexity.     Example 1:   Input: nums = [1,3,5,6], target = 5 Output: 2   Example 2:   Input: nums = [1,3,5,6], target = 2 Output: 1   Example 3:   Input: nums = [1,3,5,6], target = 7 Output: 4      Constraints:   * 1 <= nums.length <= 104  * -104 <= nums[i] <= 104  * nums contains distinct values sorted in ascending order.  * -104 <= target <= 104"
url: "https://leetcode.com/problems/search-insert-position/"
favicon: ""
aspectRatio: "52"
```


```cpp
class Solution {
    public int searchInsert(int[] nums, int target) {
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            if (nums[i] >= target) {
                return i;
            }
        }
        return n; // insert at the end
    }
}

```

