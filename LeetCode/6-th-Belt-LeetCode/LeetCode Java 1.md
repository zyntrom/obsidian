## 31. Next Permutation

### Array Manipulation

```embed
title: "Next Permutation - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Next Permutation - A permutation of an array of integers is an arrangement of its members into a sequence or linear order.   * For example, for arr = [1,2,3], the following are all the permutations of arr: [1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1].  The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).   * For example, the next permutation of arr = [1,2,3] is [1,3,2].  * Similarly, the next permutation of arr = [2,3,1] is [3,1,2].  * While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.  Given an array of integers nums, find the next permutation of nums.  The replacement must be in place [http://en.wikipedia.org/wiki/In-place_algorithm] and use only constant extra memory.     Example 1:   Input: nums = [1,2,3] Output: [1,3,2]   Example 2:   Input: nums = [3,2,1] Output: [1,2,3]   Example 3:   Input: nums = [1,1,5] Output: [1,5,1]      Constraints:   * 1 <= nums.length <= 100  * 0 <= nums[i] <= 100"
url: "https://leetcode.com/problems/next-permutation/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int n = nums.length;
        int i = n - 2;
        // Step 1: Find first decreasing element from right
        while (i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }
        if (i >= 0) {
            // Step 2: Find element just larger than nums[i]
            int j = n - 1;
            while (nums[j] <= nums[i]) {
                j--;
            }
            // Step 3: Swap
            swap(nums, i, j);
        }
        // Step 4: Reverse the suffix
        reverse(nums, i + 1, n - 1);
    }
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    private void reverse(int[] nums, int left, int right) {
        while (left < right) {
            swap(nums, left++, right--);
        }
    }
}

```

## 50. Pow(x, n)

### Divide and Conquer

```embed
title: "Pow(x, n) - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Pow(x, n) - Implement pow(x, n) [http://www.cplusplus.com/reference/valarray/pow/], which calculates x raised to the power n (i.e., xn).     Example 1:   Input: x = 2.00000, n = 10 Output: 1024.00000   Example 2:   Input: x = 2.10000, n = 3 Output: 9.26100   Example 3:   Input: x = 2.00000, n = -2 Output: 0.25000 Explanation: 2-2 = 1/22 = 1/4 = 0.25      Constraints:   * -100.0 < x < 100.0  * -231 <= n <= 231-1  * n is an integer.  * Either x is not zero or n > 0.  * -104 <= xn <= 104"
url: "https://leetcode.com/problems/powx-n/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public double myPow(double x, int n) {
        long N = n;            // convert to long to avoid overflow
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }
        return fastPow(x, N);
    }
    private double fastPow(double x, long n) {
        if (n == 0) return 1.0;
        double half = fastPow(x, n / 2);
        if (n % 2 == 0) {
            return half * half;
        } else {
            return half * half * x;
        }
    }
}

```

## 1040. Moving Stones Until Consecutive II

### Greedy/Sliding Window

```embed
title: "Moving Stones Until Consecutive II - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Moving Stones Until Consecutive II - There are some stones in different positions on the X-axis. You are given an integer array stones, the positions of the stones.  Call a stone an endpoint stone if it has the smallest or largest position. In one move, you pick up an endpoint stone and move it to an unoccupied position so that it is no longer an endpoint stone.   * In particular, if the stones are at say, stones = [1,2,5], you cannot move the endpoint stone at position 5, since moving it to any position (such as 0, or 3) will still keep that stone as an endpoint stone.  The game ends when you cannot make any more moves (i.e., the stones are in three consecutive positions).  Return an integer array answer of length 2 where:   * answer[0] is the minimum number of moves you can play, and  * answer[1] is the maximum number of moves you can play.     Example 1:   Input: stones = [7,4,9] Output: [1,2] Explanation: We can move 4 -> 8 for one move to finish the game. Or, we can move 9 -> 5, 4 -> 6 for two moves to finish the game.   Example 2:   Input: stones = [6,5,4,3,10] Output: [2,3] Explanation: We can move 3 -> 8 then 10 -> 7 to finish the game. Or, we can move 3 -> 7, 4 -> 8, 5 -> 9 to finish the game. Notice we cannot move 10 -> 2 to finish the game, because that would be an illegal move.      Constraints:   * 3 <= stones.length <= 104  * 1 <= stones[i] <= 109  * All the values of stones are unique."
url: "https://leetcode.com/problems/moving-stones-until-consecutive-ii/description/"
favicon: ""
aspectRatio: "52"
```

```java
import java.util.Arrays;

class Solution {
    public int[] numMovesStonesII(int[] stones) {
        Arrays.sort(stones);
        int x = stones[0], y = stones[1], z = stones[2];
        // Maximum moves
        int maxMoves = (y - x - 1) + (z - y - 1);
        // Minimum moves
        int minMoves;
        if (y - x == 1 && z - y == 1) {
            minMoves = 0;  // already consecutive
        } else if (y - x <= 2 || z - y <= 2) {
            minMoves = 1;  // one move enough
        } else {
            minMoves = 2;  // otherwise need 2 moves
        }
        return new int[]{minMoves, maxMoves};
    }
}

```

## 2592. Maximize Greatness of an Array

### Greedy/Sorting

```java
import java.util.Arrays;

class Solution {
    public int maximizeGreatness(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        int i = 0, j = 0, greatness = 0;

        while (i < n && j < n) {
            if (nums[j] > nums[i]) {
                greatness++;
                i++;
                j++;
            } else {
                j++;
            }
        }

        return greatness;
    }
}

```