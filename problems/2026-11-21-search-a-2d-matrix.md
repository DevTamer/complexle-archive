# Search a 2D Matrix

**Puzzle date:** 2026-11-21  
**Category:** binary search  
**Time complexity:** `O(log(m * n))`  
**Space complexity:** `O(1)`

## Explanation

The matrix is treated as one flat sorted array of m * n entries, with mid // n and mid % n converting a flat index back into a row and column. The loop is therefore a single binary search over m * n elements, halving the range each time for O(log(m * n)) — equivalently O(log m + log n). Answering O(m + n) is the natural guess, matching the staircase walk used when rows and columns are only individually sorted; this stronger fully-sorted layout allows the faster search. Space is O(1), since only index variables are kept and the matrix is never copied.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def search_matrix(matrix: list[list[int]], target: int) -> bool:
    if not matrix:
        return False

    m, n = len(matrix), len(matrix[0])
    left, right = 0, m * n
    while left < right:
        mid = left + (right - left) // 2
        if matrix[mid // n][mid % n] >= target:
            right = mid
        else:
            left = mid + 1

    return left < m * n and matrix[left // n][left % n] == target
```

### C++

```cpp
bool searchMatrix(std::vector<std::vector<int>>& matrix, int target) {
    if (matrix.empty()) {
        return false;
    }

    int m = matrix.size();
    int n = matrix[0].size();
    int left = 0, right = m * n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (matrix[mid / n][mid % n] >= target) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left < m * n && matrix[left / n][left % n] == target;
}
```

### Rust

```rust
fn search_matrix(matrix: &[Vec<i32>], target: i32) -> bool {
    if matrix.is_empty() {
        return false;
    }

    let m = matrix.len();
    let n = matrix[0].len();
    let mut left: usize = 0;
    let mut right: usize = m * n;
    while left < right {
        let mid = left + (right - left) / 2;
        if matrix[mid / n][mid % n] >= target {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    left < m * n && matrix[left / n][left % n] == target
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/search-a-2d-matrix.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
