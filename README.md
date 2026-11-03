# Merge-Sorted-Array
You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, along with two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.
# LeetCode 88: Merge Sorted Array

## Problem Description
You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, along with two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums1` and `nums2` into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be **modified in-place** inside the array `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to `0` and should be ignored.

## Solution Approach
The optimal approach is to fill `nums1` starting from the **back** (`m + n - 1`) and move backwards. This prevents overwriting any valid elements in `nums1` before they are compared. 

1. Initialize three pointers:
   - `i` pointing to the last valid element in `nums1` (`m - 1`).
   - `j` pointing to the last element in `nums2` (`n - 1`).
   - `k` pointing to the last index of the combined array (`m + n - 1`).
2. Compare the elements at `nums1[i]` and `nums2[j]`, putting the larger one at `nums1[k]`, and decrementing the respective pointers.
3. If elements remain in `nums2` after `nums1` is exhausted (`i < 0`), copy them over directly. (Elements left in `nums1` are already in their correct places).

## Python Code

```python
class Solution:
    def merge(self, nums1: list[int], m: int, nums2: list[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        i = m - 1
        j = n - 1
        k = m + n - 1
        
        # While there are still elements in nums2
        while j >= 0:
            if i >= 0 and nums1[i] > nums2[j]:
                nums1[k] = nums1[i]
                i -= 1
            else:
                nums1[k] = nums2[j]
                j -= 1
            k -= 1

# --- Local Verification / Main Execution Block ---
if __name__ == "__main__":
    solution = Solution()
    
    # Test Case 1
    nums1_ex1 = [1, 2, 3, 0, 0, 0]
    m_ex1 = 3
    nums2_ex1 = [2, 5, 6]
    n_ex1 = 3
    solution.merge(nums1_ex1, m_ex1, nums2_ex1, n_ex1)
    print(f"Test Case 1 Output: {nums1_ex1}")  # Expected: [1, 2, 2, 3, 5, 6]
    
    # Test Case 2
    nums1_ex2 = [1]
    m_ex2 = 1
    nums2_ex2 = []
    n_ex2 = 0
    solution.merge(nums1_ex2, m_ex2, nums2_ex2, n_ex2)
    print(f"Test Case 2 Output: {nums1_ex2}")  # Expected: [1]
    
    # Test Case 3
    nums1_ex3 = [0]
    m_ex3 = 0
    nums2_ex3 = [1]
    n_ex3 = 1
    solution.merge(nums1_ex3, m_ex3, nums2_ex3, n_ex3)
    print(f"Test Case 3 Output: {nums1_ex3}")  # Expected: [1]
```

## Complexity Analysis
- **Time Complexity:** $O(m + n)$ — Each element from both arrays is evaluated and placed into position exactly once.
- **Space Complexity:** $O(1)$ — The algorithm performs the operations in-place without utilizing any extra data structures.
