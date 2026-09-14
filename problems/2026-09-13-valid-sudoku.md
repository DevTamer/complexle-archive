# Valid Sudoku

**Puzzle date:** 2026-09-13  
**Category:** arrays  
**Time complexity:** `O(1)`  
**Space complexity:** `O(1)`

## Explanation

The board is fixed at 9x9, so every loop (rows, columns, and 3x3 boxes) runs a constant number of times regardless of any variable input size, and each is_valid_list call processes at most 9 elements. Since there's no growing input parameter n that these loops scale with, the total work done is a fixed constant, giving O(1) time. It's tempting to call this O(n^2) because of the nested loops over 9x9 cells, but since 9 is a hardcoded constant rather than a variable n, the nested iteration doesn't scale with any input size and stays constant. Similarly, the space used by the temporary lists and sets inside is_valid_list is bounded by 9 elements at most, so it never grows beyond a constant amount, making space O(1) as well.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def is_valid_sudoku(board: list[list[str]]) -> bool:
    def is_valid_list(xs: list[str]) -> bool:
        xs = [x for x in xs if x != '.']
        return len(set(xs)) == len(xs)

    for i in range(9):
        if not is_valid_list([board[i][j] for j in range(9)]) or \
           not is_valid_list([board[j][i] for j in range(9)]):
            return False
    for i in range(3):
        for j in range(3):
            if not is_valid_list([board[m][n] for n in range(3 * j, 3 * j + 3)
                                                for m in range(3 * i, 3 * i + 3)]):
                return False
    return True
```

### C++

```cpp
using namespace std;

bool anyDuplicate(const vector<vector<char>>& board, int start_row, int end_row,
                   int start_col, int end_col) {
    bitset<9> is_present;
    for (int i = start_row; i < end_row; ++i) {
        for (int j = start_col; j < end_col; ++j) {
            if (board[i][j] != '.') {
                if (is_present[board[i][j] - '1']) {
                    return true;
                }
                is_present.flip(board[i][j] - '1');
            }
        }
    }
    return false;
}

bool isValidSudoku(vector<vector<char>>& board) {
    for (int i = 0; i < 9; ++i) {
        if (anyDuplicate(board, i, i + 1, 0, 9)) {
            return false;
        }
    }
    for (int j = 0; j < 9; ++j) {
        if (anyDuplicate(board, 0, 9, j, j + 1)) {
            return false;
        }
    }
    for (int i = 0; i < 9; i += 3) {
        for (int j = 0; j < 9; j += 3) {
            if (anyDuplicate(board, i, i + 3, j, j + 3)) {
                return false;
            }
        }
    }
    return true;
}
```

### Rust

```rust
fn any_duplicate(board: &[Vec<char>], start_row: usize, end_row: usize, start_col: usize, end_col: usize) -> bool {
    let mut is_present = [false; 9];
    for i in start_row..end_row {
        for j in start_col..end_col {
            let c = board[i][j];
            if c != '.' {
                let idx = (c as u8 - b'1') as usize;
                if is_present[idx] {
                    return true;
                }
                is_present[idx] = true;
            }
        }
    }
    false
}

fn is_valid_sudoku(board: &[Vec<char>]) -> bool {
    for i in 0..9 {
        if any_duplicate(board, i, i + 1, 0, 9) {
            return false;
        }
    }
    for j in 0..9 {
        if any_duplicate(board, 0, 9, j, j + 1) {
            return false;
        }
    }
    for i in (0..9).step_by(3) {
        for j in (0..9).step_by(3) {
            if any_duplicate(board, i, i + 3, j, j + 3) {
                return false;
            }
        }
    }
    true
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/valid-sudoku.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
