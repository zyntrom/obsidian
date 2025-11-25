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

##