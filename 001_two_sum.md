Two Sum
=======

### Problem
https://leetcode.com/problems/two-sum/description/

### Solution 

```go
func twoSum(nums []int, target int) []int {
  // Maps from a number to its index in the array
  cache := make(map[int]int)
  for i, num := range nums {
    diff := target - num
    if index, found := cache[diff]; found {
      return []int {index, i}
    }
    cache[num] = i
  }
  return nil
}
```