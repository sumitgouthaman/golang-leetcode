[Previous](002_add_two_numbers.md) | [Home](README.md)

Longest Substring Without Repeating Characters
==============================================

### Problem
https://leetcode.com/problems/longest-substring-without-repeating-characters/description/

### Solution

```go
func Max(x, y int) int {
    if x > y {
        return x
    }
    return y
}

func lengthOfLongestSubstring(s string) int {
  max_found := 0
  lookback := make(map[rune]int)
  current_window := 0
  for pos, char := range s {
    last_occurence, found := lookback[char]
    lookback[char] = pos
    if !found {
      current_window += 1
      max_found = Max(max_found, current_window)
      continue
    }
    
    if pos - current_window <= last_occurence {
      current_window = pos - last_occurence
    } else {
      current_window += 1
      max_found = Max(max_found, current_window)
    }
  }
  
  return max_found
}
```