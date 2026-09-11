# Spiral Matrix

**Puzzle date:** 2026-07-12  
**Category:** arrays  
**Time complexity:** `O(m*n)`  
**Space complexity:** `O(m*n)`

## Explanation

The dominant cost is the set of for-loops inside the while loop, which together visit every element in the matrix exactly once. Because each cell is appended to the result exactly one time regardless of the spiral path taken, the total work is proportional to the total number of elements, m*n (rows times columns). You might be tempted to say O((m+n)²) because the while loop runs roughly (m+n)/2 times and each iteration does O(m+n) work, but that product still simplifies to O(m*n), not a larger expression. For space, the result list stores every element of the matrix, so it grows to size m*n; the boundary variables (top, bottom, left, right) are O(1) extra, making the output list the dominant space cost.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def spiral_order(matrix: list[list[int]]) -> list[int]:
    result = []
    if not matrix:
        return result
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1
    while top <= bottom and left <= right:
        for j in range(left, right + 1):
            result.append(matrix[top][j])
        top += 1
        for i in range(top, bottom + 1):
            result.append(matrix[i][right])
        right -= 1
        if top <= bottom:
            for j in range(right, left - 1, -1):
                result.append(matrix[bottom][j])
            bottom -= 1
        if left <= right:
            for i in range(bottom, top - 1, -1):
                result.append(matrix[i][left])
            left += 1
    return result
```

### C++

```cpp
#include <vector>

std::vector<int> spiralOrder(std::vector<std::vector<int>>& matrix) {
    std::vector<int> result;
    if (matrix.empty()) return result;
    int top = 0, bottom = matrix.size() - 1;
    int left = 0, right = matrix[0].size() - 1;
    while (top <= bottom && left <= right) {
        for (int j = left; j <= right; j++) result.push_back(matrix[top][j]);
        top++;
        for (int i = top; i <= bottom; i++) result.push_back(matrix[i][right]);
        right--;
        if (top <= bottom) {
            for (int j = right; j >= left; j--) result.push_back(matrix[bottom][j]);
            bottom--;
        }
        if (left <= right) {
            for (int i = bottom; i >= top; i--) result.push_back(matrix[i][left]);
            left++;
        }
    }
    return result;
}
```

### Rust

```rust
fn spiral_order(matrix: Vec<Vec<i32>>) -> Vec<i32> {
    let mut result = Vec::new();
    if matrix.is_empty() {
        return result;
    }
    let (mut top, mut bottom) = (0i32, matrix.len() as i32 - 1);
    let (mut left, mut right) = (0i32, matrix[0].len() as i32 - 1);
    while top <= bottom && left <= right {
        for j in left..=right {
            result.push(matrix[top as usize][j as usize]);
        }
        top += 1;
        for i in top..=bottom {
            result.push(matrix[i as usize][right as usize]);
        }
        right -= 1;
        if top <= bottom {
            for j in (left..=right).rev() {
                result.push(matrix[bottom as usize][j as usize]);
            }
            bottom -= 1;
        }
        if left <= right {
            for i in (top..=bottom).rev() {
                result.push(matrix[i as usize][left as usize]);
            }
            left += 1;
        }
    }
    result
}
```

---

Played daily at [complexle.com](https://complexle.com).
