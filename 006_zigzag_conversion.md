[Previous](005_longest_palindromic_substring.md) | [Home](README.md)

ZigZag Conversion
=================

### Problem
https://leetcode.com/problems/zigzag-conversion/description/

### Solution

```go
import (
  "bytes"
)

func convert(s string, numRows int) string {
  if numRows == 1 {
    return s
  }
  
  rowBuffers := make([]bytes.Buffer, numRows)
  
  for index, bufIndex, dir := 0, 0, 1; index < len(s); index, bufIndex = index + 1, bufIndex + dir {
    rowBuffers[bufIndex].WriteByte(s[index])
    
    if (bufIndex == 0 && dir == -1) || (bufIndex == numRows-1 && dir == 1) {
      dir *= -1
    }
  }
  
  var result string
  for _, buffer := range rowBuffers {
    result += buffer.String()
  }
  
  return result
}
```