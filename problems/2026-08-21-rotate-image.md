# Rotate Image

**Puzzle date:** 2026-08-21  
**Category:** arrays  
**Time complexity:** `O(n^2)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost comes from the two nested loops that iterate over the n x n matrix: the anti-diagonal mirror loop touches roughly half the cells and the horizontal mirror loop touches all cells, both giving work proportional to n^2 since n is the matrix side length. You might be tempted to think it's O(n) because the outer loop only runs n times, but you have to remember the inner loop also runs on the order of n times, multiplying out to n^2 total swaps. Space stays O(1) because the rotation is done in place using only temporary variables for swapping, with no extra arrays or lists sized by n created. A common mistake is assuming O(n) or O(n^2) space because a matrix of that size is involved, but that memory belongs to the input, not to any additional space your code allocates.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def rotate(matrix: list[list[int]]) -> list[list[int]]:
    n = len(matrix)

    # anti-diagonal mirror
    for i in range(n):
        for j in range(n - i):
            matrix[i][j], matrix[n-1-j][n-1-i] = matrix[n-1-j][n-1-i], matrix[i][j]

    # horizontal mirror
    for i in range(n // 2):
        for j in range(n):
            matrix[i][j], matrix[n-1-i][j] = matrix[n-1-i][j], matrix[i][j]

    return matrix
```

### C++

```cpp
std::vector<std::vector<int>> rotate(std::vector<std::vector<int>>& matrix) {
    int n = matrix.size();

    // anti-diagonal mirror
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n - i; ++j) {
            std::swap(matrix[i][j], matrix[n-1-j][n-1-i]);
        }
    }

    // horizontal mirror
    for (int i = 0; i < n / 2; ++i) {
        for (int j = 0; j < n; ++j) {
            std::swap(matrix[i][j], matrix[n-1-i][j]);
        }
    }

    return matrix;
}
```

### Rust

```rust
fn rotate(mut matrix: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
    let n = matrix.len();

    // anti-diagonal mirror
    for i in 0..n {
        for j in 0..(n - i) {
            let tmp = matrix[i][j];
            matrix[i][j] = matrix[n-1-j][n-1-i];
            matrix[n-1-j][n-1-i] = tmp;
        }
    }

    // horizontal mirror
    for i in 0..(n / 2) {
        for j in 0..n {
            let tmp = matrix[i][j];
            matrix[i][j] = matrix[n-1-i][j];
            matrix[n-1-i][j] = tmp;
        }
    }

    matrix
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/rotate-image.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
