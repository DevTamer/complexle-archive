# Rotting Oranges

**Puzzle date:** 2026-06-25  
**Category:** graph  
**Time complexity:** `O(m*n)`  
**Space complexity:** `O(m*n)`

## Explanation

The dominant cost is the BFS traversal of the grid, where m and n are the number of rows and columns. Every cell in the grid is visited at most once — rotten oranges are added to the queue exactly once and fresh oranges are converted to rotten (value 2) before being enqueued, preventing re-processing. You might be tempted to say O((m*n)²) because there's a while loop containing a for loop over 4 directions, but the 4-directional check is a constant factor and each cell is enqueued at most once, so the total work across all iterations is proportional to m*n. The space complexity is also O(m*n) because in the worst case (e.g., all cells are rotten from the start) the queue could hold every cell in the grid simultaneously.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
from collections import deque

def oranges_rotting(grid: list[list[int]]) -> int:
    rows, cols = len(grid), len(grid[0])
    queue = deque()
    fresh = 0
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == 2: queue.append((r, c, 0))
            elif grid[r][c] == 1: fresh += 1
    minutes = 0
    while queue:
        r, c, t = queue.popleft()
        minutes = t
        for dr, dc in [(1,0),(-1,0),(0,1),(0,-1)]:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == 1:
                grid[nr][nc] = 2
                fresh -= 1
                queue.append((nr, nc, t + 1))
    return minutes if fresh == 0 else -1
```

### C++

```cpp
#include <vector>
#include <queue>

int orangesRotting(std::vector<std::vector<int>>& grid) {
    int rows = grid.size(), cols = grid[0].size();
    std::queue<std::tuple<int,int,int>> q;
    int fresh = 0;
    for (int r = 0; r < rows; r++)
        for (int c = 0; c < cols; c++) {
            if (grid[r][c] == 2) q.push({r, c, 0});
            else if (grid[r][c] == 1) fresh++;
        }
    int minutes = 0, dr[] = {1,-1,0,0}, dc[] = {0,0,1,-1};
    while (!q.empty()) {
        auto [r, c, t] = q.front(); q.pop();
        minutes = t;
        for (int d = 0; d < 4; d++) {
            int nr = r + dr[d], nc = c + dc[d];
            if (nr >= 0 && nr < rows && nc >= 0 && nc < cols && grid[nr][nc] == 1) {
                grid[nr][nc] = 2;
                fresh--;
                q.push({nr, nc, t + 1});
            }
        }
    }
    return fresh == 0 ? minutes : -1;
}
```

### Rust

```rust
use std::collections::VecDeque;

fn oranges_rotting(grid: &mut Vec<Vec<i32>>) -> i32 {
    let (rows, cols) = (grid.len(), grid[0].len());
    let mut queue: VecDeque<(i32, i32, i32)> = VecDeque::new();
    let mut fresh = 0;
    for r in 0..rows {
        for c in 0..cols {
            match grid[r][c] {
                2 => queue.push_back((r as i32, c as i32, 0)),
                1 => fresh += 1,
                _ => {}
            }
        }
    }
    let mut minutes = 0;
    while let Some((r, c, t)) = queue.pop_front() {
        minutes = t;
        for (dr, dc) in [(1,0),(-1,0),(0,1),(0,-1)] {
            let (nr, nc) = (r + dr, c + dc);
            if nr >= 0 && (nr as usize) < rows && nc >= 0 && (nc as usize) < cols
                && grid[nr as usize][nc as usize] == 1 {
                grid[nr as usize][nc as usize] = 2;
                fresh -= 1;
                queue.push_back((nr, nc, t + 1));
            }
        }
    }
    if fresh == 0 { minutes } else { -1 }
}
```

---

Played daily at [complexle.com](https://complexle.com).
