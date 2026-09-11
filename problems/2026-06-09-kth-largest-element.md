# Kth Largest Element

**Puzzle date:** 2026-06-09  
**Category:** heap  
**Time complexity:** `O(n log k)`  
**Space complexity:** `O(k)`

## Explanation

We iterate over all n elements, and for each element we perform a heappush and conditionally a heappop on a min-heap that is capped at size k, each of which costs O(log k), giving O(n log k) total time. The heap never grows beyond k+1 elements before the pop trims it back to k, so the auxiliary space is O(k). This approach is more efficient than sorting the full array when k << n.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
import heapq

def find_kth_largest(nums: list[int], k: int) -> int:
    heap = []
    for n in nums:
        heapq.heappush(heap, n)
        if len(heap) > k:
            heapq.heappop(heap)
    return heap[0]
```

### C++

```cpp
#include <vector>
#include <queue>

int findKthLargest(std::vector<int>& nums, int k) {
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;
    for (int n : nums) {
        minHeap.push(n);
        if ((int)minHeap.size() > k)
            minHeap.pop();
    }
    return minHeap.top();
}
```

### Rust

```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

fn find_kth_largest(nums: &[i32], k: usize) -> i32 {
    let mut heap = BinaryHeap::new();
    for &n in nums {
        heap.push(Reverse(n));
        if heap.len() > k {
            heap.pop();
        }
    }
    heap.peek().unwrap().0
}
```

---

Played daily at [complexle.com](https://complexle.com).
