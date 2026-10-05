# Game of Life

**Puzzle date:** 2026-10-04  
**Category:** arrays  
**Time complexity:** `O(m*n)`  
**Space complexity:** `O(1)`

## Explanation

You should focus on the two nested loops over i and j, which run m*n times total. Inside, there's an inner double loop over the 3x3 neighborhood, but that's bounded by a constant (at most 9 cells), so it doesn't grow with input size and just contributes a constant factor. The board is modified in place using bit tricks (storing next state in the second bit), so no extra data structures scale with input, giving constant extra space. The tempting distractor O(m*n*9) is wrong only in notation—Big-O drops constant multipliers, so it simplifies to O(m*n), not a separate complexity class.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def game_of_life(board: list[list[int]]) -> list[list[int]]:
    m = len(board)
    n = len(board[0]) if m else 0
    for i in range(m):
        for j in range(n):
            count = 0
            for I in range(max(i - 1, 0), min(i + 2, m)):
                for J in range(max(j - 1, 0), min(j + 2, n)):
                    count += board[I][J] & 1
            if (count == 4 and board[i][j]) or count == 3:
                board[i][j] |= 2
    for i in range(m):
        for j in range(n):
            board[i][j] >>= 1
    return board
```

### C++

```cpp
std::vector<std::vector<int>> gameOfLife(std::vector<std::vector<int>>& board) {
    int m = static_cast<int>(board.size());
    int n = m ? static_cast<int>(board[0].size()) : 0;
    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            int count = 0;
            for (int I = std::max(i - 1, 0); I < std::min(i + 2, m); ++I) {
                for (int J = std::max(j - 1, 0); J < std::min(j + 2, n); ++J) {
                    count += board[I][J] & 1;
                }
            }
            if ((count == 4 && board[i][j]) || count == 3) {
                board[i][j] |= 2;
            }
        }
    }
    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            board[i][j] >>= 1;
        }
    }
    return board;
}
```

### Rust

```rust
fn game_of_life(board: &mut Vec<Vec<i32>>) -> Vec<Vec<i32>> {
    let m = board.len();
    let n = if m > 0 { board[0].len() } else { 0 };
    for i in 0..m {
        for j in 0..n {
            let mut count = 0;
            let i_start = if i > 0 { i - 1 } else { 0 };
            let i_end = std::cmp::min(i + 2, m);
            let j_start = if j > 0 { j - 1 } else { 0 };
            let j_end = std::cmp::min(j + 2, n);
            for ii in i_start..i_end {
                for jj in j_start..j_end {
                    count += board[ii][jj] & 1;
                }
            }
            if (count == 4 && board[i][j] != 0) || count == 3 {
                board[i][j] |= 2;
            }
        }
    }
    for i in 0..m {
        for j in 0..n {
            board[i][j] >>= 1;
        }
    }
    board.clone()
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/game-of-life.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
