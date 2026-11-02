# Last Stone Weight

**Puzzle date:** 2026-11-01  
**Category:** heap  
**Time complexity:** `O(n log n)`  
**Space complexity:** `O(n)`

## Explanation

heapify itself is only O(n), but the loop that follows runs n - 1 times and each iteration performs two pops and one push, every one of those costing O(log n) to restore the heap invariant. The loop therefore dominates at O(n log n). Answering O(n) is the common mistake — it credits the linear heapify and overlooks that the real work is the n heap operations after it. Space is O(n) because the negated copy of the stones list is a new list holding every element; the heap is maintained in that list rather than in the original input.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def last_stone_weight(stones: list[int]) -> int:
    max_heap = [-x for x in stones]
    heapq.heapify(max_heap)
    for _ in range(len(stones) - 1):
        x, y = -heapq.heappop(max_heap), -heapq.heappop(max_heap)
        heapq.heappush(max_heap, -abs(x - y))
    return -max_heap[0]
```

### C++

```cpp
int lastStoneWeight(std::vector<int>& stones) {
    std::priority_queue<int> max_heap(stones.begin(), stones.end());
    for (size_t i = 0; i + 1 < stones.size(); ++i) {
        int x = max_heap.top(); max_heap.pop();
        int y = max_heap.top(); max_heap.pop();
        max_heap.push(std::abs(x - y));
    }
    return max_heap.top();
}
```

### Rust

```rust
fn last_stone_weight(stones: &[i32]) -> i32 {
    let mut max_heap: BinaryHeap<i32> = stones.iter().cloned().collect();
    let n = stones.len();
    for _ in 0..n.saturating_sub(1) {
        let x = max_heap.pop().unwrap();
        let y = max_heap.pop().unwrap();
        max_heap.push((x - y).abs());
    }
    *max_heap.peek().unwrap_or(&0)
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/last-stone-weight.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
