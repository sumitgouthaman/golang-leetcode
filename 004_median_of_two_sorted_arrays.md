[Previous](003_longest_substring_without_repeating_chars.md) | [Home](README.md)

Median of Two Sorted Arrays
===========================

### Problem
https://leetcode.com/problems/median-of-two-sorted-arrays/description/

### Solution

```go
func getLowerAndIncrement(arr1, arr2 []int, i, j int) (int, int, int) {
  // Assume at least i < len(arr1) or j < len(arr2)
  var to_return int
  if (i < len(arr1) && j < len(arr2)) {
    if (arr1[i] < arr2[j]) {
      to_return = arr1[i]
      i += 1
    } else {
      to_return = arr2[j]
      j += 1
    }
  } else if i >= len(arr1) && j < len(arr2) {
    to_return = arr2[j]
    j += 1
  } else if i < len(arr1) && j >= len(arr2) {
    to_return = arr1[i]
    i += 1
  }
  return to_return, i, j
}

func findMedianSortedArrays(nums1 []int, nums2 []int) float64 {
  t := len(nums1) + len(nums2)
  numbers_needed := 1
  first_index := t / 2
  if t%2 == 0 {
    numbers_needed = 2
    first_index -= 1
  }
  
  median_sum := 0
  i , j := 0, 0
  
  for (i + j) < first_index {
    _, i, j = getLowerAndIncrement(nums1, nums2, i, j)
  }
  
  for n := 0; n < numbers_needed; n += 1 {
    var lower int
    lower, i, j = getLowerAndIncrement(nums1, nums2, i, j)
    median_sum += lower
  }
  
  return float64(median_sum) / float64(numbers_needed)
}
```