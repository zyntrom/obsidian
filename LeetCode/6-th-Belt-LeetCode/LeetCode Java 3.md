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

