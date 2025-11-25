# Backtracking --
## 17. Letter Combinations of a Phone Number

```embed
title: "Letter Combinations of a Phone Number - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Letter Combinations of a Phone Number - Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.  A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.  [https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png]     Example 1:   Input: digits = \"23\" Output: [\"ad\",\"ae\",\"af\",\"bd\",\"be\",\"bf\",\"cd\",\"ce\",\"cf\"]   Example 2:   Input: digits = \"2\" Output: [\"a\",\"b\",\"c\"]      Constraints:   * 1 <= digits.length <= 4  * digits[i] is a digit in the range ['2', '9']."
url: "https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    private static final String[] KEYPAD = {
        "", "", "abc", "def", "ghi", 
        "jkl", "mno", "pqrs", "tuv", "wxyz"
    };
    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<>();
        if (digits.length() == 0) return result;
        backtrack(result, new StringBuilder(), digits, 0);
        return result;
    }
    private void backtrack(List<String> result, StringBuilder current, String digits, int index) {
        if (index == digits.length()) {
            result.add(current.toString());
            return;
        }
        String letters = KEYPAD[digits.charAt(index) - '0'];
        for (char c : letters.toCharArray()) {
            current.append(c);
            backtrack(result, current, digits, index + 1);
            current.deleteCharAt(current.length() - 1); // undo
        }
    }
}

```

## 46. Permutations

```embed
title: "Permutations - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Permutations - Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.     Example 1:  Input: nums = [1,2,3] Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]   Example 2:  Input: nums = [0,1] Output: [[0,1],[1,0]]   Example 3:  Input: nums = [1] Output: [[1]]      Constraints:   * 1 <= nums.length <= 6  * -10 <= nums[i] <= 10  * All the integers of nums are unique."
url: "https://leetcode.com/problems/permutations/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        boolean[] used = new boolean[num.length];
        backtrack(nums, used, new ArrayList<>(), result);
        return result;
    }
    private void backtrack(int[] nums, boolean[] used, List<Integer> current, List<List<Integer>> result) {
        if (current.size() == nums.length) {
            result.add(new ArrayList<>(current));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (used[i]) continue;
            used[i] = true;
            current.add(nums[i]);
            backtrack(nums, used, current, result);
            current.remove(current.size() - 1);
            used[i] = false;
        }
    }
}

```

## 51. N-Queens

```embed
title: "N-Queens - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? N-Queens - The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.  Given an integer n, return all distinct solutions to the n-queens puzzle. You may return the answer in any order.  Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space, respectively.     Example 1:  [https://assets.leetcode.com/uploads/2020/11/13/queens.jpg]   Input: n = 4 Output: [[\".Q..\",\"...Q\",\"Q...\",\"..Q.\"],[\"..Q.\",\"Q...\",\"...Q\",\".Q..\"]] Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above   Example 2:   Input: n = 1 Output: [[\"Q\"]]      Constraints:   * 1 <= n <= 9"
url: "https://leetcode.com/problems/n-queens/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    List<List<String>> result;
    int n;
    public List<List<String>> solveNQueens(int n) {
        this.n = n;
        result = new ArrayList<>();
        boolean[] cols = new boolean[n];
        boolean[] diag1 = new boolean[2 * n];
        boolean[] diag2 = new boolean[2 * n];
        char[][] board = new char[n][n];
        for (char[] row : board)
            Arrays.fill(row, '.');
        backtrack(0, board, cols, diag1, diag2);
        return result;
    }

    private void backtrack(int row, char[][] board,
                           boolean[] cols, boolean[] diag1, boolean[] diag2) {

        if (row == n) {
            result.add(build(board));
            return;
        }
        for (int col = 0; col < n; col++) {
            int d1 = row - col + n; 
            int d2 = row + col;
            if (cols[col] || diag1[d1] || diag2[d2]) continue;
            // place queen
            board[row][col] = 'Q';
            cols[col] = diag1[d1] = diag2[d2] = true;
            backtrack(row + 1, board, cols, diag1, diag2);
            // undo
            board[row][col] = '.';
            cols[col] = diag1[d1] = diag2[d2] = false;
        }
    }
    private List<String> build(char[][] board) {
        List<String> res = new ArrayList<>();
        for (char[] row : board)
            res.add(new String(row));
        return res;
    }
}

```

## 526. Beautiful Arrangement

```embed
title: "Beautiful Arrangement - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Beautiful Arrangement - Suppose you have n integers labeled 1 through n. A permutation of those n integers perm (1-indexed) is considered a beautiful arrangement if for every i (1 <= i <= n), either of the following is true:   * perm[i] is divisible by i.  * i is divisible by perm[i].  Given an integer n, return the number of the beautiful arrangements that you can construct.     Example 1:   Input: n = 2 Output: 2 Explanation:  The first beautiful arrangement is [1,2]:     - perm[1] = 1 is divisible by i = 1     - perm[2] = 2 is divisible by i = 2 The second beautiful arrangement is [2,1]:     - perm[1] = 2 is divisible by i = 1     - i = 2 is divisible by perm[2] = 1   Example 2:   Input: n = 1 Output: 1      Constraints:   * 1 <= n <= 15"
url: "https://leetcode.com/problems/beautiful-arrangement/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    int count = 0;
    public int countArrangement(int n) {
        boolean[] used = new boolean[n + 1];
        backtrack(1, n, used);
        return count;
    }
    private void backtrack(int pos, int n, boolean[] used) {
        if (pos > n) {
            count++;
            return;
        }
        for (int num = 1; num <= n; num++) {
            if (!used[num] && (num % pos == 0 || pos % num == 0)) {
                used[num] = true;
                backtrack(pos + 1, n, used);
                used[num] = false;
            }
        }
    }
}

```

## 39. Combination Sum

```embed
title: "Combination Sum - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Combination Sum - Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.  The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.  The test cases are generated such that the number of unique combinations that sum up to target is less than 150 combinations for the given input.     Example 1:   Input: candidates = [2,3,6,7], target = 7 Output: [[2,2,3],[7]] Explanation: 2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times. 7 is a candidate, and 7 = 7. These are the only two combinations.   Example 2:   Input: candidates = [2,3,5], target = 8 Output: [[2,2,2,2],[2,3,3],[3,5]]   Example 3:   Input: candidates = [2], target = 1 Output: []      Constraints:   * 1 <= candidates.length <= 30  * 2 <= candidates[i] <= 40  * All elements of candidates are distinct.  * 1 <= target <= 40"
url: "https://leetcode.com/problems/combination-sum/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(candidates);  
        backtrack(candidates, target, 0, new ArrayList<>(), result);
        return result;
    }
    private void backtrack(int[] candidates, int target, int start, 
                           List<Integer> temp, List<List<Integer>> result) {
        if (target == 0) {
            result.add(new ArrayList<>(temp));
            return;
        }
        for (int i = start; i < candidates.length; i++) {
            if (candidates[i] > target) break;  // optimization
            temp.add(candidates[i]);
            backtrack(candidates, target - candidates[i], i, temp, result); 
            temp.remove(temp.size() - 1);
        }
    }
}

```

## 40. Combination Sum II

```embed
title: "Combination Sum II - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Combination Sum II - Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.  Each number in candidates may only be used once in the combination.  Note: The solution set must not contain duplicate combinations.     Example 1:   Input: candidates = [10,1,2,7,6,1,5], target = 8 Output:  [ [1,1,6], [1,2,5], [1,7], [2,6] ]   Example 2:   Input: candidates = [2,5,2,1,2], target = 5 Output:  [ [1,2,2], [5] ]      Constraints:   * 1 <= candidates.length <= 100  * 1 <= candidates[i] <= 50  * 1 <= target <= 30"
url: "https://leetcode.com/problems/combination-sum-ii/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(candidates); // important to skip duplicates
        backtrack(candidates, target, 0, new ArrayList<>(), result);
        return result;
    }
    private void backtrack(int[] nums, int target, int start,
            List<Integer> temp, List<List<Integer>> result) {
        if (target == 0) {
            result.add(new ArrayList<>(temp));
            return;
        }
        for (int i = start; i < nums.length; i++) {
            // 🔥 Avoid duplicates at the same tree level
            if (i > start && nums[i] == nums[i - 1]) continue;
            // If the number exceeds target, no need to continue
            if (nums[i] > target) break;
            temp.add(nums[i]);
            backtrack(nums, target - nums[i], i + 1, temp, result); 
            // move i+1 because we can't reuse
            temp.remove(temp.size() - 1);
        }
    }
}

```

## 491. Non-decreasing Subsequences

```embed
title: "Non-decreasing Subsequences - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Non-decreasing Subsequences - Given an integer array nums, return all the different possible non-decreasing subsequences of the given array with at least two elements. You may return the answer in any order.     Example 1:   Input: nums = [4,6,7,7] Output: [[4,6],[4,6,7],[4,6,7,7],[4,7],[4,7,7],[6,7],[6,7,7],[7,7]]   Example 2:   Input: nums = [4,4,3,2,1] Output: [[4,4]]      Constraints:   * 1 <= nums.length <= 15  * -100 <= nums[i] <= 100"
url: "https://leetcode.com/problems/non-decreasing-subsequences/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public List<List<Integer>> findSubsequences(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(0, nums, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(int index, int[] nums, List<Integer> path, List<List<Integer>> result) {
        if (path.size() >= 2) {
            result.add(new ArrayList<>(path));
        }
        HashSet<Integer> used = new HashSet<>(); 
        // avoid duplicates at same level
        for (int i = index; i < nums.length; i++) {
            // skip duplicates at this depth
            if (used.contains(nums[i])) continue;
            // enforce non-decreasing order
            if (!path.isEmpty() && nums[i] < path.get(path.size() - 1)) continue;
            used.add(nums[i]);    // mark used at this recursion level
            path.add(nums[i]);

            backtrack(i + 1, nums, path, result);

            path.remove(path.size() - 1);
        }
    }
}

```