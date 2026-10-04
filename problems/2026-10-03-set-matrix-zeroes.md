# Set Matrix Zeroes

**Puzzle date:** 2026-10-03  
**Category:** arrays  
**Time complexity:** `O(m*n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost comes from the nested loops that scan every cell of the matrix twice (once to mark zeros, once to apply them), where m is the number of rows and n is the number of columns. Since each loop visits every element a constant number of times, the total work scales directly with the total number of cells, giving O(m*n) time. You might be tempted to think it's O(m+n) because the algorithm uses the first row and column as markers, but that only describes the size of the marker storage, not the actual work done scanning the whole grid. Space stays O(1) because the algorithm cleverly reuses the first row and column of the input matrix itself as marker flags instead of allocating separate arrays, so no extra memory grows with the input size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def set_zeroes(matrix: list[list[int]]) -> list[list[int]]:
    first_col = any(matrix[i][0] == 0 for i in range(len(matrix)))
    first_row = any(matrix[0][j] == 0 for j in range(len(matrix[0])))

    for i in range(1, len(matrix)):
        for j in range(1, len(matrix[0])):
            if matrix[i][j] == 0:
                matrix[i][0], matrix[0][j] = 0, 0

    for i in range(1, len(matrix)):
        for j in range(1, len(matrix[0])):
            if matrix[i][0] == 0 or matrix[0][j] == 0:
                matrix[i][j] = 0

    if first_col:
        for i in range(len(matrix)):
            matrix[i][0] = 0

    if first_row:
        for j in range(len(matrix[0])):
            matrix[0][j] = 0

    return matrix
```

### C++

```cpp
std::vector<std::vector<int>> setZeroes(std::vector<std::vector<int>>& matrix) {
    if (matrix.empty() || matrix[0].empty()) {
        return matrix;
    }
    int m = matrix.size(), n = matrix[0].size();
    bool first_col = false, first_row = false;
    for (int i = 0; i < m; ++i) {
        if (matrix[i][0] == 0) first_col = true;
    }
    for (int j = 0; j < n; ++j) {
        if (matrix[0][j] == 0) first_row = true;
    }

    for (int i = 1; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }

    for (int i = 1; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                matrix[i][j] = 0;
            }
        }
    }

    if (first_col) {
        for (int i = 0; i < m; ++i) matrix[i][0] = 0;
    }
    if (first_row) {
        for (int j = 0; j < n; ++j) matrix[0][j] = 0;
    }
    return matrix;
}
```

### Rust

```rust
fn set_zeroes(matrix: &mut Vec<Vec<i32>>) -> Vec<Vec<i32>> {
    if matrix.is_empty() || matrix[0].is_empty() {
        return matrix.clone();
    }
    let m = matrix.len();
    let n = matrix[0].len();
    let mut first_col = false;
    let mut first_row = false;
    for i in 0..m {
        if matrix[i][0] == 0 {
            first_col = true;
        }
    }
    for j in 0..n {
        if matrix[0][j] == 0 {
            first_row = true;
        }
    }

    for i in 1..m {
        for j in 1..n {
            if matrix[i][j] == 0 {
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }

    for i in 1..m {
        for j in 1..n {
            if matrix[i][0] == 0 || matrix[0][j] == 0 {
                matrix[i][j] = 0;
            }
        }
    }

    if first_col {
        for i in 0..m {
            matrix[i][0] = 0;
        }
    }
    if first_row {
        for j in 0..n {
            matrix[0][j] = 0;
        }
    }
    matrix.clone()
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/set-matrix-zeroes.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
