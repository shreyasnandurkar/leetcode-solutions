#1021. Remove Outermost Parentheses

## Intuition

*   Since the String is already a valid parenthesis, we don't need a Stack to verify.
*   Initially, we set `count = 0`. If we encounter `(`, we do `count++`. If we get `)`, we do `count--`.
*   When does an outer parenthesis occur? They occur only when `count` is `0` and `(` occurs, or `count` is `1` and `)` occurs. 
*   So, we do not add the outer parenthesis in the answer String. Then, after iterating the whole input string, we return the answer.

## Solution

```java
class Solution {
    public String removeOuterParentheses(String s) {
        StringBuilder ans = new StringBuilder();
        int cnt = 0; 
        
        for (char c : s.toCharArray()) {
            if (c == '(') {
                if (cnt != 0) ans.append('(');
                cnt++;
            } else {
                if (cnt != 1) ans.append(')');
                cnt--;
            }
        }

        return ans.toString();
    }
}
```

## Complexity

*   **Time complexity:** $O(N)$ 
*   **Space complexity:** $O(N)$ (Space of the output String via `StringBuilder`).
