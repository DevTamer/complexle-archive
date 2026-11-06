# Maximal Rectangle

**Puzzle date:** 2026-11-05  
**Category:** stack  
**Time complexity:** `O(m*n)`  
**Space complexity:** `O(n)`

## Explanation

The outer loop runs once per row and the inner loop updates one histogram entry per column, which is m × n work in total. largest_rectangle_area is called once per row, but it is a monotonic stack that runs in O(n) per call — each column index is pushed and popped at most once — so those calls add another m × n rather than something quadratic in n. Space is only O(n): the heights array and the stack are both sized by the number of columns and are reused across rows. Answering O(m*n) for space is the natural trap, since the matrix itself is that large, but no copy of it is ever made.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def maximal_rectangle(matrix: list[list[str]]) -> int:
    def largest_rectangle_area(heights: list[int]) -> int:
        stk = [-1]
        result = 0
        for i in range(len(heights) + 1):
            while stk[-1] != -1 and (i == len(heights) or heights[stk[-1]] >= heights[i]):
                h = heights[stk.pop()]
                result = max(result, h * ((i - 1) - stk[-1]))
            stk.append(i)
        return result

    if not matrix:
        return 0
    result = 0
    heights = [0] * len(matrix[0])
    for i in range(len(matrix)):
        for j in range(len(matrix[0])):
            heights[j] = heights[j] + 1 if matrix[i][j] == '1' else 0
        result = max(result, largest_rectangle_area(heights))
    return result
```

### C++

```cpp
int largestRectangleArea(const std::vector<int>& heights) {
    std::vector<int> stk = {-1};
    int result = 0;
    int n = static_cast<int>(heights.size());
    for (int i = 0; i <= n; ++i) {
        while (stk.back() != -1 && (i == n || heights[stk.back()] >= heights[i])) {
            int last = stk.back(); stk.pop_back();
            result = std::max(result, heights[last] * ((i - 1) - stk.back()));
        }
        stk.push_back(i);
    }
    return result;
}

int maximalRectangle(std::vector<std::vector<char>>& matrix) {
    if (matrix.empty() || matrix[0].empty()) {
        return 0;
    }
    int result = 0;
    std::vector<int> heights(matrix[0].size(), 0);
    for (size_t i = 0; i < matrix.size(); ++i) {
        for (size_t j = 0; j < matrix[0].size(); ++j) {
            heights[j] = matrix[i][j] == '1' ? heights[j] + 1 : 0;
        }
        result = std::max(result, largestRectangleArea(heights));
    }
    return result;
}
```

### Rust

```rust
fn largest_rectangle_area(heights: &[i32]) -> i32 {
    let mut stk: Vec<i32> = vec![-1];
    let mut result = 0;
    let n = heights.len() as i32;
    for i in 0..=n {
        while *stk.last().unwrap() != -1
            && (i == n || heights[*stk.last().unwrap() as usize] >= heights[i as usize])
        {
            let last = stk.pop().unwrap();
            let h = heights[last as usize];
            result = result.max(h * ((i - 1) - *stk.last().unwrap()));
        }
        stk.push(i);
    }
    result
}

fn maximal_rectangle(matrix: &[Vec<char>]) -> i32 {
    if matrix.is_empty() || matrix[0].is_empty() {
        return 0;
    }
    let mut result = 0;
    let mut heights = vec![0; matrix[0].len()];
    for i in 0..matrix.len() {
        for j in 0..matrix[0].len() {
            heights[j] = if matrix[i][j] == '1' { heights[j] + 1 } else { 0 };
        }
        result = result.max(largest_rectangle_area(&heights));
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/maximal-rectangle.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
