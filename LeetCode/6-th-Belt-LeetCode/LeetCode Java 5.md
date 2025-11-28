# Stack

## 735. Asteroid Collision

```embed
title: "Asteroid Collision - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Asteroid Collision - We are given an array asteroids of integers representing asteroids in a row. The indices of the asteroid in the array represent their relative position in space.  For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.  Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.     Example 1:   Input: asteroids = [5,10,-5] Output: [5,10] Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide.   Example 2:   Input: asteroids = [8,-8] Output: [] Explanation: The 8 and -8 collide exploding each other.   Example 3:   Input: asteroids = [10,2,-5] Output: [10] Explanation: The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.   Example 4:   Input: asteroids = [3,5,-6,2,-1,4]​​​​​​​ Output: [-6,2,4] Explanation: The asteroid -6 makes the asteroid 3 and 5 explode, and then continues going left. On the other side, the asteroid 2 makes the asteroid -1 explode and then continues going right, without reaching asteroid 4.      Constraints:   * 2 <= asteroids.length <= 104  * -1000 <= asteroids[i] <= 1000  * asteroids[i] != 0"
url: "https://leetcode.com/problems/asteroid-collision/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Stack<Integer> st = new Stack<>();
        for (int a : asteroids) {
            boolean alive = true;
            while (alive && a < 0 && !st.isEmpty() && st.peek() > 0) {
                int top = st.peek();
                if (top < -a) {
                    st.pop();        // top explodes, keep checking
                } else if (top == -a) {
                    st.pop();        // both explode
                    alive = false;
                } else {
                    alive = false;   // current asteroid explodes
                }
            }
            if (alive) st.push(a);
        }
        int[] res = new int[st.size()];
        for (int i = res.length - 1; i >= 0; i--) {
            res[i] = st.pop();
        }
        return res;
    }
}

```

## 150. Evaluate Reverse Polish Notation

```embed
title: "Evaluate Reverse Polish Notation - LeetCode"
image: "https://leetcode.com/static/images/LeetCode_Sharing.png"
description: "Can you solve this real interview question? Evaluate Reverse Polish Notation - You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation [http://en.wikipedia.org/wiki/Reverse_Polish_notation].  Evaluate the expression. Return an integer that represents the value of the expression.  Note that:   * The valid operators are '+', '-', '*', and '/'.  * Each operand may be an integer or another expression.  * The division between two integers always truncates toward zero.  * There will not be any division by zero.  * The input represents a valid arithmetic expression in a reverse polish notation.  * The answer and all the intermediate calculations can be represented in a 32-bit integer.     Example 1:   Input: tokens = [\"2\",\"1\",\"+\",\"3\",\"*\"] Output: 9 Explanation: ((2 + 1) * 3) = 9   Example 2:   Input: tokens = [\"4\",\"13\",\"5\",\"/\",\"+\"] Output: 6 Explanation: (4 + (13 / 5)) = 6   Example 3:   Input: tokens = [\"10\",\"6\",\"9\",\"3\",\"+\",\"-11\",\"*\",\"/\",\"*\",\"17\",\"+\",\"5\",\"+\"] Output: 22 Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5 = ((10 * (6 / (12 * -11))) + 17) + 5 = ((10 * (6 / -132)) + 17) + 5 = ((10 * 0) + 17) + 5 = (0 + 17) + 5 = 17 + 5 = 22      Constraints:   * 1 <= tokens.length <= 104  * tokens[i] is either an operator: \"+\", \"-\", \"*\", or \"/\", or an integer in the range [-200, 200]."
url: "https://leetcode.com/problems/evaluate-reverse-polish-notation/description/"
favicon: ""
aspectRatio: "52"
```

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> st = new Stack<>();
        for (String token : tokens) {
            if (token.equals("+")) {
                st.push(st.pop() + st.pop());
            } else if (token.equals("-")) {
                int b = st.pop(), a = st.pop();
                st.push(a - b);
            } else if (token.equals("*")) {
                st.push(st.pop() * st.pop());
            } else if (token.equals("/")) {
                int b = st.pop(), a = st.pop();
                st.push(a / b);
            } else {
                st.push(Integer.parseInt(token));
            }
        }
        return st.pop();
    }
}
```

