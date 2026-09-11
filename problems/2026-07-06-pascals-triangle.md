# Pascal's Triangle

**Puzzle date:** 2026-07-06  
**Category:** arrays  
**Time complexity:** `O(n²)`  
**Space complexity:** `O(n²)`

## Explanation

The dominant cost comes from the two nested loops: the outer loop runs n times (once per row), and the inner loop for row i runs roughly i times, giving a total of 1 + 2 + 3 + ... + n = n*(n+1)/2 operations, which is O(n²). The inner loop `for j in range(1, i)` is the specific construct that drives this — it grows linearly with each row index i. For space, you store the entire triangle in `result`, which holds 1 + 2 + ... + n = n*(n+1)/2 integers total, also O(n²). The most tempting wrong answer for both time and space is O(n), because you might only count the outer loop or think only about the number of rows rather than the total number of elements across all rows.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def generate_pascals_triangle(num_rows: int) -> list[list[int]]:
    result = []
    for i in range(num_rows):
        row = [1] * (i + 1)
        for j in range(1, i):
            row[j] = result[i - 1][j - 1] + result[i - 1][j]
        result.append(row)
    return result
```

### C++

```cpp
#include <vector>

std::vector<std::vector<int>> generatePascalsTriangle(int numRows) {
    std::vector<std::vector<int>> result;
    for (int i = 0; i < numRows; i++) {
        std::vector<int> row(i + 1, 1);
        for (int j = 1; j < i; j++) {
            row[j] = result[i - 1][j - 1] + result[i - 1][j];
        }
        result.push_back(row);
    }
    return result;
}
```

### Rust

```rust
fn generate_pascals_triangle(num_rows: usize) -> Vec<Vec<i32>> {
    let mut result: Vec<Vec<i32>> = Vec::new();
    for i in 0..num_rows {
        let mut row = vec![1; i + 1];
        for j in 1..i {
            row[j] = result[i - 1][j - 1] + result[i - 1][j];
        }
        result.push(row);
    }
    result
}
```

---

Played daily at [complexle.com](https://complexle.com).
