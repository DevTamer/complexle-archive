# Top K Frequent Elements

**Puzzle date:** 2026-07-17  
**Category:** heap  
**Time complexity:** `O(n log k)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the loop over all unique elements in 'counts', where each iteration performs a heap push and occasionally a heap pop — both costing O(log k) since the heap is kept at most size k. You iterate over at most n unique elements (in the worst case all elements are distinct), giving O(n log k) total. The Counter construction is O(n) which is dominated by the heap operations when k is not trivially small. You might be tempted to say O(n log n) because sorting-based solutions are common for this problem, but this heap-based approach caps heap size at k, making each operation O(log k) rather than O(log n). For space, the Counter can hold up to n entries in the worst case (all elements distinct), making it O(n), which dominates the O(k) heap; choosing O(k) ignores the space used by the frequency map.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
import heapq
from collections import Counter

def top_k_frequent(nums: list[int], k: int) -> list[int]:
    counts = Counter(nums)
    heap = []
    for num, freq in counts.items():
        heapq.heappush(heap, (freq, num))
        if len(heap) > k:
            heapq.heappop(heap)
    return [num for freq, num in heap]
```

### C++

```cpp
#include <vector>
#include <queue>
#include <unordered_map>
#include <functional>

std::vector<int> topKFrequent(std::vector<int>& nums, int k) {
    std::unordered_map<int, int> counts;
    for (int n : nums) counts[n]++;
    std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, std::greater<>> minHeap;
    for (auto& [num, freq] : counts) {
        minHeap.push({freq, num});
        if ((int)minHeap.size() > k) minHeap.pop();
    }
    std::vector<int> result;
    while (!minHeap.empty()) {
        result.push_back(minHeap.top().second);
        minHeap.pop();
    }
    return result;
}
```

### Rust

```rust
use std::cmp::Reverse;
use std::collections::{BinaryHeap, HashMap};

fn top_k_frequent(nums: &[i32], k: usize) -> Vec<i32> {
    let mut counts: HashMap<i32, i32> = HashMap::new();
    for &n in nums {
        *counts.entry(n).or_insert(0) += 1;
    }
    let mut heap: BinaryHeap<Reverse<(i32, i32)>> = BinaryHeap::new();
    for (&num, &freq) in counts.iter() {
        heap.push(Reverse((freq, num)));
        if heap.len() > k {
            heap.pop();
        }
    }
    heap.into_iter().map(|Reverse((_, num))| num).collect()
}
```

---

Played daily at [complexle.com](https://complexle.com).
