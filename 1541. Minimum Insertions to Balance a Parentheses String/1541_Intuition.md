# Minimum Insertions to Balance a Parentheses String

## Intuition

* `cnt` tracks the number of right parentheses `)` currently needed. `ans` tracks the total number of manual insertions made.
* Each `(` requires two `)`, adding `+2` to `cnt`. Each `)` fulfills one requirement, subtracting `-1` from `cnt`.
* If `cnt == 0` and `ch == ')'`: We have a right bracket but no open left bracket. We must insert a `(`, which adds `+1` to `ans`. Inserting this `(` means we now need two `)`, so we add `+2` to `cnt`. 
* If `cnt % 2 == 1` and `ch == '('`: An odd `cnt` means the previous `(` only has one matching `)` so far. We must close it before opening a new `(`. We insert the missing `)`, adding `+1` to `ans` and subtracting `1` from `cnt` to fulfill that requirement.
* After checking these edge cases, we apply the standard character updates: `cnt -= 1` if `ch == ')'`, else `cnt += 2`.
* At the end of the string, any remaining `cnt` represents missing `)` that must be inserted to close the remaining `(`, so we add `cnt` to `ans`.

## Solution

```java
class Solution {
    public int minInsertions(String s) {
        int ans = 0, cnt = 0;

        for(char ch : s.toCharArray()){
            if(cnt == 0 && ch == ')'){
                ans += 1;
                cnt += 2;
            }
            else if(cnt % 2 == 1 && ch == '('){
                ans += 1;
                cnt -= 1;
            }

            if(ch == ')') cnt -= 1;
            else cnt += 2;
        }

        ans += cnt;
        return ans;
    }
}
```

## Complexity

* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$ (Since we are not using any extra data structures)
