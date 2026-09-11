# Course Schedule (Topological Sort)

**Puzzle date:** 2026-06-11  
**Category:** graph  
**Time complexity:** `O(V + E)`  
**Space complexity:** `O(V + E)`

## Explanation

This is Kahn's algorithm for topological sort. We iterate over all prerequisites once to build the adjacency list and in-degree array (O(E)), then process each node and edge exactly once in the BFS loop (O(V + E)), giving a total time complexity of O(V + E) where V = num_courses and E = len(prerequisites). The space complexity is also O(V + E) because we store the adjacency list (O(V + E)), the in-degree array (O(V)), and the BFS queue which holds at most O(V) nodes.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
from collections import deque

def can_finish(num_courses: int, prerequisites: list[list[int]]) -> bool:
    in_degree = [0] * num_courses
    adj = [[] for _ in range(num_courses)]
    for a, b in prerequisites:
        adj[b].append(a)
        in_degree[a] += 1
    queue = deque(i for i in range(num_courses) if in_degree[i] == 0)
    completed = 0
    while queue:
        node = queue.popleft()
        completed += 1
        for neighbor in adj[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    return completed == num_courses
```

### C++

```cpp
#include <vector>
#include <queue>

bool canFinish(int numCourses, std::vector<std::vector<int>>& prerequisites) {
    std::vector<int> inDegree(numCourses, 0);
    std::vector<std::vector<int>> adj(numCourses);
    for (auto& p : prerequisites) {
        adj[p[1]].push_back(p[0]);
        inDegree[p[0]]++;
    }
    std::queue<int> q;
    for (int i = 0; i < numCourses; i++)
        if (inDegree[i] == 0) q.push(i);
    int completed = 0;
    while (!q.empty()) {
        int node = q.front(); q.pop();
        completed++;
        for (int nb : adj[node])
            if (--inDegree[nb] == 0) q.push(nb);
    }
    return completed == numCourses;
}
```

### Rust

```rust
use std::collections::VecDeque;

fn can_finish(num_courses: usize, prerequisites: &[(usize, usize)]) -> bool {
    let mut in_degree = vec![0usize; num_courses];
    let mut adj = vec![vec![]; num_courses];
    for &(a, b) in prerequisites {
        adj[b].push(a);
        in_degree[a] += 1;
    }
    let mut queue: VecDeque<usize> = (0..num_courses)
        .filter(|&i| in_degree[i] == 0)
        .collect();
    let mut completed = 0;
    while let Some(node) = queue.pop_front() {
        completed += 1;
        for &nb in &adj[node] {
            in_degree[nb] -= 1;
            if in_degree[nb] == 0 { queue.push_back(nb); }
        }
    }
    completed == num_courses
}
```

---

Played daily at [complexle.com](https://complexle.com).
