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

## 22. Generate Parentheses

```embed
title: "Generate Parentheses - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Generate Parentheses - Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.     Example 1:  Input: n = 3 Output: [\"((()))\",\"(()())\",\"(())()\",\"()(())\",\"()()()\"]   Example 2:  Input: n = 1 Output: [\"()\"]      Constraints:   * 1 <= n <= 8"
url: "https://leetcode.com/problems/generate-parentheses/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, new StringBuilder(), 0, 0, n);
        return result;
    }
    private void backtrack(List<String> result, StringBuilder sb, int open, int close, int n) {
        // if the constructed string is of length 2*n, it's a valid combo
        if (sb.length() == 2 * n) {
            result.add(sb.toString());
            return;
        }
        // add '(' if we can still place more opens
        if (open < n) {
            sb.append('(');
            backtrack(result, sb, open + 1, close, n);
            sb.deleteCharAt(sb.length() - 1);
        }
        // add ')' if close < open
        if (close < open) {
            sb.append(')');
            backtrack(result, sb, open, close + 1, n);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```

## 79. Word Search

```embed
title: "Word Search - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Word Search - Given an m x n grid of characters board and a string word, return true if word exists in the grid.  The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.     Example 1:  [https://assets.leetcode.com/uploads/2020/11/04/word2.jpg]   Input: board = [[\"A\",\"B\",\"C\",\"E\"],[\"S\",\"F\",\"C\",\"S\"],[\"A\",\"D\",\"E\",\"E\"]], word = \"ABCCED\" Output: true   Example 2:  [https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg]   Input: board = [[\"A\",\"B\",\"C\",\"E\"],[\"S\",\"F\",\"C\",\"S\"],[\"A\",\"D\",\"E\",\"E\"]], word = \"SEE\" Output: true   Example 3:  [https://assets.leetcode.com/uploads/2020/10/15/word3.jpg]   Input: board = [[\"A\",\"B\",\"C\",\"E\"],[\"S\",\"F\",\"C\",\"S\"],[\"A\",\"D\",\"E\",\"E\"]], word = \"ABCB\" Output: false      Constraints:   * m == board.length  * n = board[i].length  * 1 <= m, n <= 6  * 1 <= word.length <= 15  * board and word consists of only lowercase and uppercase English letters.     Follow up: Could you use search pruning to make your solution faster with a larger board?"
url: "https://leetcode.com/problems/word-search/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        int m = board.length, n = board[0].length;
        char[] w = word.toCharArray();

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == w[0] && dfs(board, i, j, w, 0)) {
                    return true;
                }
            }
        }
        return false;
    }
    private boolean dfs(char[][] board, int i, int j, char[] w, int k) {
        if (board[i][j] != w[k]) return false;
        if (k == w.length - 1) return true;
        char tmp = board[i][j];
        board[i][j] = '#'; // mark visited
        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
        for (int[] d : dirs) {
            int ni = i + d[0], nj = j + d[1];
            if (ni >= 0 && ni < board.length && nj >= 0 && nj < board[0].length && board[ni][nj] != '#') {
                if (dfs(board, ni, nj, w, k + 1)) {
                    board[i][j] = tmp;
                    return true;
                }
            }
        }
        board[i][j] = tmp; // unmark
        return false;
    }
}

```

## 131. Palindrome Partitioning

```embed
title: "Palindrome Partitioning - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Palindrome Partitioning - Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.     Example 1:  Input: s = \"aab\" Output: [[\"a\",\"a\",\"b\"],[\"aa\",\"b\"]]   Example 2:  Input: s = \"a\" Output: [[\"a\"]]      Constraints:   * 1 <= s.length <= 16  * s contains only lowercase English letters."
url: "https://leetcode.com/problems/palindrome-partitioning/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> res = new ArrayList<>();
        backtrack(0, s, new ArrayList<>(), res);
        return res;
    }
    private void backtrack(int start, String s, List<String> path, List<List<String>> res) {
        if (start == s.length()) {
            res.add(new ArrayList<>(path));
            return;
        }

        for (int end = start; end < s.length(); end++) {
            if (isPalindrome(s, start, end)) {
                path.add(s.substring(start, end + 1));
                backtrack(end + 1, s, path, res);
                path.remove(path.size() - 1);
            }
        }
    }
    private boolean isPalindrome(String s, int l, int r) {
        while (l < r) {
            if (s.charAt(l++) != s.charAt(r--)) return false;
        }
        return true;
    }
}

```

## 78. Subsets

```embed
title: "Subsets - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Subsets - Given an integer array nums of unique elements, return all possible subsets (the power set).  The solution set must not contain duplicate subsets. Return the solution in any order.     Example 1:   Input: nums = [1,2,3] Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]   Example 2:   Input: nums = [0] Output: [[],[0]]      Constraints:   * 1 <= nums.length <= 10  * -10 <= nums[i] <= 10  * All the numbers of nums are unique."
url: "https://leetcode.com/problems/subsets/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(0, nums, new ArrayList<>(), res);
        return res;
    }

    private void backtrack(int index, int[] nums, List<Integer> path, List<List<Integer>> res) {
        res.add(new ArrayList<>(path));

        for (int i = index; i < nums.length; i++) {
            path.add(nums[i]);
            backtrack(i + 1, nums, path, res);
            path.remove(path.size() - 1);
        }
    }
}

```

## 1239. Maximum Length of a Concatenated String with Unique Characters

```embed
title: "Maximum Length of a Concatenated String with Unique Characters - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Maximum Length of a Concatenated String with Unique Characters - You are given an array of strings arr. A string s is formed by the concatenation of a subsequence of arr that has unique characters.  Return the maximum possible length of s.  A subsequence is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.     Example 1:   Input: arr = [\"un\",\"iq\",\"ue\"] Output: 4 Explanation: All the valid concatenations are: - \"\" - \"un\" - \"iq\" - \"ue\" - \"uniq\" (\"un\" + \"iq\") - \"ique\" (\"iq\" + \"ue\") Maximum length is 4.   Example 2:   Input: arr = [\"cha\",\"r\",\"act\",\"ers\"] Output: 6 Explanation: Possible longest valid concatenations are \"chaers\" (\"cha\" + \"ers\") and \"acters\" (\"act\" + \"ers\").   Example 3:   Input: arr = [\"abcdefghijklmnopqrstuvwxyz\"] Output: 26 Explanation: The only string in arr has all 26 characters.      Constraints:   * 1 <= arr.length <= 16  * 1 <= arr[i].length <= 26  * arr[i] contains only lowercase English letters."
url: "https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    int max = 0;
    public int maxLength(List<String> arr) {
        backtrack(arr, 0, "", 0);
        return max;
    }
    private void backtrack(List<String> arr, int index, String current, int length) {
        max = Math.max(max, length);
        for (int i = index; i < arr.size(); i++) {
            String next = arr.get(i);
            if (isUnique(current, next)) {
                backtrack(arr, i + 1, current + next, length + next.length());
            }
        }
    }
    private boolean isUnique(String current, String next) {
        int[] freq = new int[26];
        for (char c : current.toCharArray()) {
            freq[c - 'a']++;
        }
        for (char c : next.toCharArray()) {
            if (freq[c - 'a']++ > 0) return false;
        }
        return true;
    }
}
```

## 1219. Path with Maximum Gold

```embed
title: "Path with Maximum Gold - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Path with Maximum Gold - In a gold mine grid of size m x n, each cell in this mine has an integer representing the amount of gold in that cell, 0 if it is empty.  Return the maximum amount of gold you can collect under the conditions:   * Every time you are located in a cell you will collect all the gold in that cell.  * From your position, you can walk one step to the left, right, up, or down.  * You can't visit the same cell more than once.  * Never visit a cell with 0 gold.  * You can start and stop collecting gold from any position in the grid that has some gold.     Example 1:   Input: grid = [[0,6,0],[5,8,7],[0,9,0]] Output: 24 Explanation: [[0,6,0],  [5,8,7],  [0,9,0]] Path to get the maximum gold, 9 -> 8 -> 7.   Example 2:   Input: grid = [[1,0,7],[2,0,6],[3,4,5],[0,3,0],[9,0,20]] Output: 28 Explanation: [[1,0,7],  [2,0,6],  [3,4,5],  [0,3,0],  [9,0,20]] Path to get the maximum gold, 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7.      Constraints:   * m == grid.length  * n == grid[i].length  * 1 <= m, n <= 15  * 0 <= grid[i][j] <= 100  * There are at most 25 cells containing gold."
url: "https://leetcode.com/problems/path-with-maximum-gold/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {

    public int getMaximumGold(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int max = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] != 0) {
                    max = Math.max(max, dfs(grid, i, j));
                }
            }
        }
        return max;
    }
    private int dfs(int[][] grid, int i, int j) {
        if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] == 0)
            return 0;
        int gold = grid[i][j];
        grid[i][j] = 0;  // mark visited
        int up = dfs(grid, i - 1, j);
        int down = dfs(grid, i + 1, j);
        int left = dfs(grid, i, j - 1);
        int right = dfs(grid, i, j + 1);
        grid[i][j] = gold; // unmark
        return gold + Math.max(Math.max(up, down), Math.max(left, right));
    }
}

```