# Number of Islands

**Puzzle date:** 2026-06-08  
**Category:** graph  
**Time complexity:** `O(m*n)`  
**Space complexity:** `O(m*n)`

## Explanation

Every cell in the m×n grid is visited at most once by the outer loop and DFS combined, since visited cells are marked '0' immediately, giving O(m*n) time. The space complexity is O(m*n) in the worst case due to the DFS recursion stack, which can reach depth m*n when the entire grid is one large island (e.g., a snake-shaped path covering all cells).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def num_islands(grid: list[list[str]]) -> int:
    if not grid:
        return 0
    rows, cols = len(grid), len(grid[0])
    count = 0

    def dfs(r, c):
        if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] != '1':
            return
        grid[r][c] = '0'
        for dr, dc in [(1,0),(-1,0),(0,1),(0,-1)]:
            dfs(r+dr, c+dc)

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                dfs(r, c)
                count += 1
    return count
```

### C++

```cpp
void dfs(std::vector<std::vector<char>>& grid, int r, int c) {
    int rows = grid.size(), cols = grid[0].size();
    if (r < 0 || r >= rows || c < 0 || c >= cols || grid[r][c] != '1')
        return;
    grid[r][c] = '0';
    dfs(grid, r+1, c); dfs(grid, r-1, c);
    dfs(grid, r, c+1); dfs(grid, r, c-1);
}

int numIslands(std::vector<std::vector<char>>& grid) {
    if (grid.empty()) return 0;
    int count = 0;
    for (int r = 0; r < grid.size(); r++)
        for (int c = 0; c < grid[0].size(); c++)
            if (grid[r][c] == '1') { dfs(grid, r, c); count++; }
    return count;
}
```

### Rust

```rust
fn num_islands(grid: &mut Vec<Vec<char>>) -> i32 {
    let (rows, cols) = (grid.len(), grid[0].len());
    let mut count = 0;

    fn dfs(grid: &mut Vec<Vec<char>>, r: i32, c: i32) {
        let (rows, cols) = (grid.len() as i32, grid[0].len() as i32);
        if r < 0 || r >= rows || c < 0 || c >= cols { return; }
        if grid[r as usize][c as usize] != '1' { return; }
        grid[r as usize][c as usize] = '0';
        for (dr, dc) in [(1,0),(-1,0),(0,1),(0,-1)] {
            dfs(grid, r + dr, c + dc);
        }
    }

    for r in 0..rows {
        for c in 0..cols {
            if grid[r][c] == '1' { dfs(grid, r as i32, c as i32); count += 1; }
        }
    }
    count
}
```

---

Played daily at [complexle.com](https://complexle.com).
