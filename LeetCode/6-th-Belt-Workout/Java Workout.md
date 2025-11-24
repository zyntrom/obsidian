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

## 3.