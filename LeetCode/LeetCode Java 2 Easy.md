## 11. Length of Last Word

```cpp
class Solution {
    public int lengthOfLastWord(String s) {
        int n = s.length();
        int count = 0;
        int p = n - 1;
        // Find the index of the last non-space character
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) != ' ') {
                p = i;
            }
        }
        // Count characters of the last word backwards
        for (int i = p; i >= 0; i--) {
            if (s.charAt(i) == ' ') {
                break;
            }
            count++;
        }
        return count;
    }
}

```

## 12. Plus One

```java
class Solution {
    public int[] plusOne(int[] digits) {
        int n = digits.length;
        // Traverse from last digit
        for (int i = n - 1; i >= 0; i--) {
            // If digit is less than 9, simply increment and return
            if (digits[i] < 9) {
                digits[i]++;
                return digits;
            }
            
            // If digit is 9, set it to 0 and continue loop (carry)
            digits[i] = 0;
        }
        // If all digits were 9, we need an extra leading 1
        int[] result = new int[n + 1];
        result[0] = 1; // rest will be 0 by default
        return result;
    }
}

```

## 13. Add Binary

```java
class Solution {
    public String addBinary(String a, String b) {
        StringBuilder result = new StringBuilder();
        
        int i = a.length() - 1;
        int j = b.length() - 1;
        int carry = 0;
        // Loop through both strings from right to left
        while (i >= 0 || j >= 0 || carry == 1) {
            int sum = carry;
            if (i >= 0) {
                sum += a.charAt(i--) - '0'; // convert char to int
            }
            if (j >= 0) {
                sum += b.charAt(j--) - '0';
            }
            // Append the current bit (sum % 2)
            result.append(sum % 2);
            // Update carry
            carry = sum / 2;
        }
        // Reverse the result to get correct order
        return result.reverse().toString();
    }
}

```

## 14. Sqrt(x)

```java
class Solution {
    public int mySqrt(int x) {
        if (x < 2) return x;
        int left = 1, right = x / 2;
        int ans = 0;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            long sq = (long) mid * mid; // avoid overflow
            if (sq == x) {
                return mid;
            } else if (sq < x) {
                ans = mid;       // store last valid value
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return ans;
    }
}

```

## 15. Climbing Stairs

```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) return n;
        int a = 1; // ways to reach step 1
        int b = 2; // ways to reach step 2
        for (int i = 3; i <= n; i++) {
            int c = a + b; // current ways
            a = b;        // shift
            b = c;        // shift
        }
        return b;
    }
}

```

## 16. Remove Duplicates from Sorted List

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) return null;
        ListNode current = head;
        while (current != null && current.next != null) {
            if (current.val == current.next.val) {
                // skip the duplicate
                current.next = current.next.next;
            } else {
                current = current.next; // move forward
            }
        }
        return head;
    }
}

```

## 17. Merge Sorted Array

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m - 1;      // pointer for nums1
        int j = n - 1;      // pointer for nums2
        int k = m + n - 1;  // pointer for final position
        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }
        // If nums2 still has remaining elements
        while (j >= 0) {
            nums1[k--] = nums2[j--];
        }
    }
}

```

## 18. Binary Tree Inorder Traversal

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        inorder(root, result);
        return result;
    }
    private void inorder(TreeNode node, List<Integer> result) {
        if (node == null) return;
        
        inorder(node.left, result);   // Left
        result.add(node.val);         // Root
        inorder(node.right, result);  // Right
    }
}

```

## 19. Same Tree

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        // Both nodes are null → trees match here
        if (p == null && q == null) return true;
        // One is null and the other is not → mismatch
        if (p == null || q == null) return false;
        // Values don't match → mismatch
        if (p.val != q.val) return false;
        // Check left subtree AND right subtree
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}

```

## 20. Symmetric Tree

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return isMirror(root.left, root.right);
    }
    private boolean isMirror(TreeNode t1, TreeNode t2) {
        // If both nodes are null → symmetric
        if (t1 == null && t2 == null) return true;
        // One is null but not the other → not symmetric
        if (t1 == null || t2 == null) return false;
        // Values must match AND subtrees must be mirrors
        return (t1.val == t2.val)
            && isMirror(t1.left, t2.right)
            && isMirror(t1.right, t2.left);
    }
}

```

