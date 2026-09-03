
## Intuition

- If we have all even or all odd elements then it's `true` obviously.
- If the array contains both types of elements, then we can convert them ONLY to odd elements because if we try to convert all to even elements, then one even element will be left out at the last.
- Conversion to odd elements of the entire array is only possible if all even elements can be converted to odd elements.
- Which means the smallest odd element in the array must be smaller than the smallest even element so that the `arr[i] >= 1` condition is always upheld.

## Solution

```java
class Solution {
    public boolean uniformArray(int[] nums1) {
        int n = nums1.length;
        int odd = Integer.MAX_VALUE;
        int even = Integer.MAX_VALUE;
        
        for (int i = 0; i < n; i++) {
            if (nums1[i] % 2 == 0) {
                even = Math.min(even, nums1[i]);
            } else {
                odd = Math.min(odd, nums1[i]);
            }
        }

        if (odd == Integer.MAX_VALUE || even == Integer.MAX_VALUE || odd < even) {
            return true;
        }
        
        return false;
    }
}
```

## Complexity

- **Time complexity:** `O(N)`
- **Space complexity:** `O(1)`
