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

## 5. Increasing Subsequences

```java
import java.util.ArrayList;
import java.util.List;
import java.util.HashSet;

class Solution {
    public List<List<Integer>> findSubsequences(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> current = new ArrayList<Integer>();
        backtrack(0, nums, current, result);
        return result;
    }
    private void backtrack(int index, int[] nums, List<Integer> current, List<List<Integer>> result) {
        if (current.size() >= 2) {
            // add a copy of current
            List<Integer> temp = new ArrayList<Integer>(current);
            result.add(temp);
        }
        // To avoid duplicates at the same depth
        HashSet<Integer> used = new HashSet<Integer>();
        for (int i = index; i < nums.length; i++) {
            // If we already tried nums[i] at this level, skip
            if (used.contains(nums[i])) {
                continue;
            }
            // If current is not empty, ensure non-decreasing order
            if (current.size() > 0) {
                int last = current.get(current.size() - 1);
                if (nums[i] < last) {
                    continue;
                }
            }
            used.add(nums[i]);  // mark value used at this depth
            current.add(nums[i]);
            backtrack(i + 1, nums, current, result);
            current.remove(current.size() - 1); // backtrack
        }
    }
}

```

## 6.Push Dominoes

```java
class Solution {
    public String pushDominoes(String dominoes) {
        int n = dominoes.length();
        char[] arr = dominoes.toCharArray();
        int lastPos = -1;      // last seen index of 'L' or 'R'
        char lastChar = 'L';   // pretend before start there is 'L'
        int i = 0;
        while (i <= n) {
            char currentChar;
            if (i == n) {
                currentChar = 'R';     // treat end like a right push
            } else {
                currentChar = arr[i];
            }
            if (currentChar != '.') {
                // Case 1: same direction: L....L   or   R....R
                if (currentChar == lastChar) {
                    int k = lastPos + 1;
                    while (k < i) {
                        arr[k] = currentChar;
                        k++;
                    }
                }
                // Case 2: R....L (inward collapse)
                else if (lastChar == 'R' && currentChar == 'L') {
                    int left = lastPos + 1;
                    int right = i - 1;
                    while (left < right) {
                        arr[left] = 'R';
                        arr[right] = 'L';
                        left++;
                        right--;
                    }
                }
                // Case 3: L....R  (do nothing → they stay '.')
                lastPos = i;
                lastChar = currentChar;
            }
            i++;
        }
        return new String(arr);
    }
}

```

## 7. Boats to Save People

```java
class Solution {
    public int numRescueBoats(int[] people, int limit) {
        // Sort the array first
        java.util.Arrays.sort(people);
        int left = 0;
        int right = people.length - 1;
        int boats = 0;
        while (left <= right) {
            // If light + heavy fits, take both
            if (people[left] + people[right] <= limit) {
                left++;      // move light pointer
                right--;     // move heavy pointer
            } else {
                // heavy person goes alone
                right--;
            }
            boats++; // one boat used every iteration
        }
        return boats;
    }
}

```

## 8.Letter Combinations of a Phone Number

```java
class Solution {
    private String[] mapping = {
        "",     // 0
        "",     // 1
        "abc",  // 2
        "def",  // 3
        "ghi",  // 4
        "jkl",  // 5
        "mno",  // 6
        "pqrs", // 7
        "tuv",  // 8
        "wxyz"  // 9
    };
    public List<String> letterCombinations(String digits) {
        List<String> result = new ArrayList<String>();
        if (digits == null || digits.length() == 0) {
            return result;
        }
        backtrack(digits, 0, "", result);
        return result;
    }
    private void backtrack(String digits, int index, String current, List<String> result) {
        if (index == digits.length()) {
            result.add(current);
            return;
        }
        int digit = digits.charAt(index) - '0';
        String letters = mapping[digit];
        for (int i = 0; i < letters.length(); i++) {
            char ch = letters.charAt(i);
            backtrack(digits, index + 1, current + ch, result);
        }
    }
}

```

## 9.Maximize the Confusion of an Exam

```java
class Solution {

    public int maxConsecutiveAnswers(String s, int k) {
        int maxT = longestChar(s, k, 'T');
        int maxF = longestChar(s, k, 'F');
        return Math.max(maxT, maxF);
    }
    // find longest substring that can be turned into char 'ch'
    private int longestChar(String s, int k, char ch) {
        int left = 0;
        int countFlips = 0;
        int maxLen = 0;
        for (int right = 0; right < s.length(); right++) {
            if (s.charAt(right) != ch) {
                countFlips++;  // we need to flip this
            }
            // shrink window if flips exceed k
            while (countFlips > k) {
                if (s.charAt(left) != ch) {
                    countFlips--;
                }
                left++;
            }
            int windowLen = right - left + 1;
            if (windowLen > maxLen) {
                maxLen = windowLen;
            }
        }
        return maxLen;
    }
}

```

## 10.Gold Mine Problem

```java
class Solution {
    public int maxGold(int[][] mine) {
        int n = mine.length;       // number of rows
        int m = mine[0].length;    // number of columns
        // DP array
        int[][] dp = new int[n][m];
        // Fill last column first
        for (int i = 0; i < n; i++) {
            dp[i][m - 1] = mine[i][m - 1];
        }
        // Fill from right → left
        for (int col = m - 2; col >= 0; col--) {
            for (int row = 0; row < n; row++) {
                int right = dp[row][col + 1];
                int rightUp = 0;
                int rightDown = 0;
                // check boundaries
                if (row - 1 >= 0) {
                    rightUp = dp[row - 1][col + 1];
                }
                if (row + 1 < n) {
                    rightDown = dp[row + 1][col + 1];
                }
                // choose best
                int bestNext = Math.max(right, Math.max(rightUp, rightDown));
                dp[row][col] = mine[row][col] + bestNext;
            }
        }
        // answer will be max of first column
        int maxGold = 0;
        for (int i = 0; i < n; i++) {
            maxGold = Math.max(maxGold, dp[i][0]);
        }
        return maxGold;
    }
}

```

## 11.Koko Eating Bananas

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int left = 1;
        int right = getMaxPile(piles); // max pile = upper limit
        int answer = right;
        while (left <= right) {
            int mid = left + (right - left) / 2;  // mid = eating speed
            int hoursNeeded = getHours(piles, mid);
            if (hoursNeeded <= h) {
                // mid might be the answer; try slower speed
                answer = mid;
                right = mid - 1;
            } else {
                // too slow, need to increase speed
                left = mid + 1;
            }
        }
        return answer;
    }
    // Helper: find maximum pile value
    private int getMaxPile(int[] piles) {
        int max = 0;
        for (int i = 0; i < piles.length; i++) {
            if (piles[i] > max) {
                max = piles[i];
            }
        }
        return max;
    }
    // Helper: compute total hours needed for speed k
    private int getHours(int[] piles, int k) {
        int hours = 0;
        for (int i = 0; i < piles.length; i++) {
            int pile = piles[i];
            // Work out how many hours this pile takes
            // hours += ceil(pile / k)
            hours += (pile + k - 1) / k;
        }
        return hours;
    }
}

```

## 12.Three Sum Closest

```java
import java.util.*;

class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length;
        // Start with any possible sum
        int closestSum = nums[0] + nums[1] + nums[2];
        for (int i = 0; i < n - 2; i++) {
            int left = i + 1;
            int right = n - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                // Check if this is closer to the target
                if (Math.abs(sum - target) < Math.abs(closestSum - target)) {
                    closestSum = sum;
                }
                if (sum < target) {
                    left++;     // need a larger sum
                } else if (sum > target) {
                    right--;    // need a smaller sum
                } else {
                    // exactly equal → best possible
                    return sum;
                }
            }
        }
        return closestSum;
    }
}

```

## 13.Permutation Sequence

```java
import java.util.*;

class Solution {
    public String getPermutation(int n, int k) {
        // list of available numbers
        List<Integer> nums = new ArrayList<>();
        for (int i = 1; i <= n; i++) {
            nums.add(i);
        }
        // factorial table
        int[] fact = new int[n + 1];
        fact[0] = 1;
        for (int i = 1; i <= n; i++) {
            fact[i] = fact[i - 1] * i;
        }
        // answer string
        StringBuilder result = new StringBuilder();
        // convert k to zero-based index
        int index = k - 1;
        // build permutation
        for (int i = n; i > 0; i--) {
            int blockSize = fact[i - 1];
            int selected = index / blockSize;
            // append the selected number
            result.append(nums.get(selected));
            // remove it from list
            nums.remove(selected);
            // update index for next position
            index = index % blockSize;
        }
        return result.toString();
    }
}
```

## 14.Divide Players Into Teams of Equal Skill

```java

```