## 1.Permutation in String

```java
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if (s1.length() > s2.length()) {
            return false;
        }
        int[] s1Count = new int[26];
        int[] s2Count = new int[26];
        // Count characters of s1 using basic loop
        for (int i = 0; i < s1.length(); i++) {
            char c = s1.charAt(i);
            s1Count[c - 'a']++;
        }
        int window = s1.length();
        // Count first window in s2
        for (int i = 0; i < window; i++) {
            char c = s2.charAt(i);
            s2Count[c - 'a']++;
        }
        // Check initial window
        if (matches(s1Count, s2Count)) {
            return true;
        }
        // Sliding window
        for (int i = window; i < s2.length(); i++) {
            // Add new character to window
            char add = s2.charAt(i);
            s2Count[add - 'a']++;
            // Remove character leaving the window
            char remove = s2.charAt(i - window);
            s2Count[remove - 'a']--;
            // Check match
            if (matches(s1Count, s2Count)) {
                return true;
            }
        }
        return false;
    }
    // Compare arrays with basic loop
    private boolean matches(int[] a, int[] b) {
        for (int i = 0; i < 26; i++) {
            if (a[i] != b[i]) {
                return false;
            }
        }
        return true;
    }
}

```

## 2.Count increasing pairs

```java
class Solution {
    public int countIncreasingPairs(int[] arr) {
        int n = arr.length;
        int count = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (arr[i] < arr[j]) {
                    count++;
                }
            }
        }
        return count;
    }
}

```

## 3.Beautiful Arrangements

```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public List<List<Integer>> beautifulArrangements(int n) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (n <= 0) {
            return result;
        }
        boolean[] used = new boolean[n + 1]; // index 1..n
        List<Integer> current = new ArrayList<Integer>();
        dfs(1, n, used, current, result);
        return result;
    }
    private void dfs(int pos, int n, boolean[] used, List<Integer> current, List<List<Integer>> result) {
        if (pos > n) {
            // reached a full valid permutation; add a copy
            List<Integer> copy = new ArrayList<Integer>(current);
            result.add(copy);
            return;
        }
        // try every number from 1..n
        for (int num = 1; num <= n; num++) {
            if (used[num]) {
                continue;
            }
            // check beautiful condition at position pos
            if (num % pos == 0 || pos % num == 0) {
                // choose
                used[num] = true;
                current.add(num);
                // recurse to next position
                dfs(pos + 1, n, used, current, result);
                // backtrack
                current.remove(current.size() - 1);
                used[num] = false;
            }
        }
    }
    // quick test
    public static void main(String[] args) {
        Solution s = new Solution();
        int n = 3;
        List<List<Integer>> perms = s.beautifulArrangements(n);
        System.out.println("Count: " + perms.size());
        for (int i = 0; i < perms.size(); i++) {
            System.out.println(perms.get(i));
        }
    }
}

```

## 4.Partition Equal Subset Sum

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int total = 0;
        for (int i = 0; i < nums.length; i++) {
            total += nums[i];
        }
        // If total sum is odd, cannot split equally
        if (total % 2 != 0) {
            return false;
        }
        int target = total / 2;
        // dp[i] means: can we make sum i using some elements
        boolean[] dp = new boolean[target + 1];
        dp[0] = true;  // sum 0 is always possible
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            // go backwards to avoid using same number twice
            for (int s = target; s >= num; s--) {
                if (dp[s - num]) {
                    dp[s] = true;
                }
            }
        }
        return dp[target];
    }
}

```

## 5.