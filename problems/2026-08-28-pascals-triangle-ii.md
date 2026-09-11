# Pascal's Triangle II

**Puzzle date:** 2026-08-28  
**Category:** arrays  
**Time complexity:** `O(n²)`  
**Space complexity:** `O(n)`

## Explanation

You should look at the two nested loops here: the outer loop runs row_index+1 times, and for each outer step i, the inner loop runs i times. That means the total number of inner-loop operations adds up like 1+2+3+...+n, which is a triangular number and simplifies to O(n²). It's tempting to call this O(n) because there's only one array being built, but that ignores the fact that the inner loop's work grows with each outer iteration rather than staying constant. For space, the algorithm only allocates one list of size row_index+1 to store the result, so the extra space used (beyond the required output) is O(n), not O(n²) or O(1), since the array size scales directly with n.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def get_row(row_index: int) -> list[int]:
    result = [0] * (row_index + 1)
    for i in range(row_index + 1):
        old = result[0] = 1
        for j in range(1, i + 1):
            old, result[j] = result[j], old + result[j]
    return result
```

### C++

```cpp
#include <vector>

std::vector<int> getRow(int rowIndex) {
    std::vector<int> result(rowIndex + 1);
    for (int i = 0; i < (int)result.size(); ++i) {
        int prev_result = result[0] = 1;
        for (int j = 1; j <= i; ++j) {
            int tmp = result[j];
            result[j] += prev_result;
            prev_result = tmp;
        }
    }
    return result;
}
```

### Rust

```rust
fn get_row(row_index: i32) -> Vec<i32> {
    let n = (row_index + 1) as usize;
    let mut result = vec![0i32; n];
    for i in 0..n {
        result[0] = 1;
        let mut old = 1;
        for j in 1..=i {
            let tmp = result[j];
            result[j] = old + tmp;
            old = tmp;
        }
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/pascals-triangle-ii.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
