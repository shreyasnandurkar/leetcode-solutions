## Intuition

- The `max[0...i] = max(nums[i], max[0...i-1])` so we don't need a prefix array to store the maximum value.
- The `min[i...n-1] = min(nums[i], min[i+1...n-1])`. We need a suffix array to store the minimum value; we can't avoid it. 
- Now we loop from `0` to `n-1`. The very first index `i` we get where `max[0...i] - min[i...n-1] <= k`, we return `i`.
- At the end, we return `-1` if no index meets the condition.

## Solution

```java
class Solution {
    public int firstStableIndex(int[] nums, int k) {
        int n = nums.length;
        int[] minisuf = new int[n];
        minisuf[n-1] = nums[n-1];
        
        for (int i = n - 2; i >= 0; i--) {
            minisuf[i] = Math.min(minisuf[i + 1], nums[i]);
        }
        
        int maxipre = Integer.MIN_VALUE;

        for (int i = 0; i < n; i++) {
            maxipre = Math.max(maxipre, nums[i]);
            if (maxipre - minisuf[i] <= k) {
                return i;
            }
        }

        return -1;
    }
}
```

## Complexity

- **Time complexity:** `O(N)`
- **Space complexity:** `O(N)`
