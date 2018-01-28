[Previous](004_median_of_two_sorted_arrays.md) | [Home](README.md) | [Next](006_zigzag_conversion.md)

Longest Palindromic Substring
=============================

### Problem
https://leetcode.com/problems/longest-palindromic-substring/description/

### Solution

```go
func longestPalindrome(s string) string {
  N := len(s)
  best := ""
  
  if N > 0 {
    best = string(s[0])
  }
    
  // Initialize a matrix of NxN bools.
  palindromeMatrix := make([][]bool, N)
  for i := range palindromeMatrix {
    palindromeMatrix[i] = make([]bool, N)
  }
    
  for i := 0; i < N; i++ {
    for j := 0; j < N; j++ {
      if j > i {
        break
      }
      palindromeMatrix[i][j] = true
    }
  }
  
  for wSize := 2; wSize <= N; wSize++ {
    for i, j := 0, wSize - 1; j < N; i, j = i+1, j+1 {
      palindromeMatrix[i][j] = (s[i] == s[j]) && palindromeMatrix[i+1][j-1]
      if palindromeMatrix[i][j] && (j-i+1 > len(best)) {
        best = s[i:j+1]
      }
    }
  }
  
  return best
}
```