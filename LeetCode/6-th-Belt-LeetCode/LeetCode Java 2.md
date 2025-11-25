## 60. Permutation Sequence

### Math/Factorial

```embed
title: "Permutation Sequence - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Permutation Sequence - The set [1, 2, 3, ..., n] contains a total of n! unique permutations.  By listing and labeling all of the permutations in order, we get the following sequence for n = 3:   1. \"123\"  2. \"132\"  3. \"213\"  4. \"231\"  5. \"312\"  6. \"321\"  Given n and k, return the kth permutation sequence.     Example 1:  Input: n = 3, k = 3 Output: \"213\"   Example 2:  Input: n = 4, k = 9 Output: \"2314\"   Example 3:  Input: n = 3, k = 1 Output: \"123\"      Constraints:   * 1 <= n <= 9  * 1 <= k <= n!"
url: "https://leetcode.com/problems/permutation-sequence/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public String getPermutation(int n, int k) {
        List<Integer> nums = new ArrayList<>();
        int[] fact = new int[n];
        
        // prepare factorials
        fact[0] = 1;
        for(int i = 1; i < n; i++) 
            fact[i] = fact[i - 1] * i;
        
        // list of numbers 1 to n
        for(int i = 1; i <= n; i++)
            nums.add(i);
        
        // convert k to 0-based index
        k--;
        StringBuilder sb = new StringBuilder();
        
        for(int i = n; i >= 1; i--) {
            int idx = k / fact[i - 1];
            sb.append(nums.get(idx));
            nums.remove(idx);
            k %= fact[i - 1];
        }
        return sb.toString();
    }
}
```

## 1823. Find the Winner of the Circular Game

### Queue/Simulation

```embed
title: "Find the Winner of the Circular Game - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Find the Winner of the Circular Game - There are n friends that are playing a game. The friends are sitting in a circle and are numbered from 1 to n in clockwise order. More formally, moving clockwise from the ith friend brings you to the (i+1)th friend for 1 <= i < n, and moving clockwise from the nth friend brings you to the 1st friend.  The rules of the game are as follows:   1. Start at the 1st friend.  2. Count the next k friends in the clockwise direction including the friend you started at. The counting wraps around the circle and may count some friends more than once.  3. The last friend you counted leaves the circle and loses the game.  4. If there is still more than one friend in the circle, go back to step 2 starting from the friend immediately clockwise of the friend who just lost and repeat.  5. Else, the last friend in the circle wins the game.  Given the number of friends, n, and an integer k, return the winner of the game.     Example 1:  [https://assets.leetcode.com/uploads/2021/03/25/ic234-q2-ex11.png]   Input: n = 5, k = 2 Output: 3 Explanation: Here are the steps of the game: 1) Start at friend 1. 2) Count 2 friends clockwise, which are friends 1 and 2. 3) Friend 2 leaves the circle. Next start is friend 3. 4) Count 2 friends clockwise, which are friends 3 and 4. 5) Friend 4 leaves the circle. Next start is friend 5. 6) Count 2 friends clockwise, which are friends 5 and 1. 7) Friend 1 leaves the circle. Next start is friend 3. 8) Count 2 friends clockwise, which are friends 3 and 5. 9) Friend 5 leaves the circle. Only friend 3 is left, so they are the winner.  Example 2:   Input: n = 6, k = 5 Output: 1 Explanation: The friends leave in this order: 5, 4, 6, 2, 3. The winner is friend 1.      Constraints:   * 1 <= k <= n <= 500     Follow up:  Could you solve this problem in linear time with constant space?"
url: "https://leetcode.com/problems/find-the-winner-of-the-circular-game/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public int findTheWinner(int n, int k) {
        int winner = 0; // 0-based index
        
        for (int i = 1; i <= n; i++) {
            winner = (winner + k) % i;
        }
        
        return winner + 1; // convert to 1-based
    }
}
```

## 53. Maximum Subarray

```embed
title: "Maximum Subarray - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Maximum Subarray - Given an integer array nums, find the subarray with the largest sum, and return its sum.     Example 1:   Input: nums = [-2,1,-3,4,-1,2,1,-5,4] Output: 6 Explanation: The subarray [4,-1,2,1] has the largest sum 6.   Example 2:   Input: nums = [1] Output: 1 Explanation: The subarray [1] has the largest sum 1.   Example 3:   Input: nums = [5,4,-1,7,8] Output: 23 Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.      Constraints:   * 1 <= nums.length <= 105  * -104 <= nums[i] <= 104     Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle."
url: "https://leetcode.com/problems/maximum-subarray/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {

    public int maxSubArray(int[] nums) {
        int currentSum = nums[0];
        int maxSum = nums[0];
        for (int i = 1; i < nums.length; i++) {
            // extend or restart
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }
        return maxSum;
    }
}

```

## 416. Partition Equal Subset Sum

```embed
title: "Partition Equal Subset Sum - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Partition Equal Subset Sum - Given an integer array nums, return true if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or false otherwise.     Example 1:   Input: nums = [1,5,11,5] Output: true Explanation: The array can be partitioned as [1, 5, 5] and [11].   Example 2:   Input: nums = [1,2,3,5] Output: false Explanation: The array cannot be partitioned into equal sum subsets.      Constraints:   * 1 <= nums.length <= 200  * 1 <= nums[i] <= 100"
url: "https://leetcode.com/problems/partition-equal-subset-sum/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int total = 0;
        for (int num : nums) total += num;
        // If total sum is odd → cannot partition
        if (total % 2 != 0) return false;
        int target = total / 2;
        boolean[] dp = new boolean[target + 1];
        dp[0] = true; // base case
        for (int num : nums) {
            for (int s = target; s >= num; s--) {
                dp[s] = dp[s] || dp[s - num];
            }
        }
        return dp[target];
    }
}

```

## 5. Longest Palindromic Substring

```embed
title: "Longest Palindromic Substring - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Longest Palindromic Substring - Given a string s, return the longest palindromic substring in s.     Example 1:   Input: s = \"babad\" Output: \"bab\" Explanation: \"aba\" is also a valid answer.   Example 2:   Input: s = \"cbbd\" Output: \"bb\"      Constraints:   * 1 <= s.length <= 1000  * s consist of only digits and English letters."
url: "https://leetcode.com/problems/longest-palindromic-substring/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public String longestPalindrome(String s) {
        int n = s.length();
        if (n < 2) return s;
        int start = 0, maxLen = 1;
        for (int i = 0; i < n; i++) {
            // odd length palindrome
            int len1 = expand(s, i, i);
            // even length palindrome
            int len2 = expand(s, i, i + 1);
            int len = Math.max(len1, len2);
            if (len > maxLen) {
                maxLen = len;
                start = i - (len - 1) / 2;
            }
        }
        return s.substring(start, start + maxLen);
    }
    private int expand(String s, int left, int right) {
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            left--;
            right++;
        }
        return right - left - 1; // palindrome length
    }
}
```

## 646. Maximum Length of Pair Chain

```embed
title: "Maximum Length of Pair Chain - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Maximum Length of Pair Chain - You are given an array of n pairs pairs where pairs[i] = [lefti, righti] and lefti < righti.  A pair p2 = [c, d] follows a pair p1 = [a, b] if b < c. A chain of pairs can be formed in this fashion.  Return the length longest chain which can be formed.  You do not need to use up all the given intervals. You can select pairs in any order.     Example 1:   Input: pairs = [[1,2],[2,3],[3,4]] Output: 2 Explanation: The longest chain is [1,2] -> [3,4].   Example 2:   Input: pairs = [[1,2],[7,8],[4,5]] Output: 3 Explanation: The longest chain is [1,2] -> [4,5] -> [7,8].      Constraints:   * n == pairs.length  * 1 <= n <= 1000  * -1000 <= lefti < righti <= 1000"
url: "https://leetcode.com/problems/maximum-length-of-pair-chain/description/"
favicon: ""
aspectRatio: "52"
```

```java
import java.util.*;

class Solution {
    public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, (a, b) -> a[1] - b[1]);  // sort by ending value
        
        int count = 1;
        int lastEnd = pairs[0][1];
        
        for (int i = 1; i < pairs.length; i++) {
            if (pairs[i][0] > lastEnd) {
                count++;
                lastEnd = pairs[i][1];
            }
        }
        
        return count;
    }
}

```

