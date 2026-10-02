# Gas Station

**Puzzle date:** 2026-10-01  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here is the single for loop that runs through every index of the gas array exactly once, doing constant-time arithmetic (subtraction, addition, comparison) on each pass. Since there's no nested loop or recursive call, the work grows linearly with the size of the input, giving you O(n) time. You might be tempted to think O(n²) because gas station problems often get brute-forced by checking every starting point with an inner loop, but this greedy single-pass version avoids that by tracking running sums instead of retesting each start. For space, only a few scalar variables (start, total_sum, current_sum, diff) are used regardless of input size, so no extra memory scales with n, making it O(1) space rather than something like O(n) that would suggest an auxiliary array or list was created.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def can_complete_circuit(gas: list[int], cost: list[int]) -> int:
    start, total_sum, current_sum = 0, 0, 0
    for i in range(len(gas)):
        diff = gas[i] - cost[i]
        current_sum += diff
        total_sum += diff
        if current_sum < 0:
            start = i + 1
            current_sum = 0
    if total_sum >= 0:
        return start
    return -1
```

### C++

```cpp
int canCompleteCircuit(std::vector<int>& gas, std::vector<int>& cost) {
    int start = 0, total_sum = 0, current_sum = 0;
    for (int i = 0; i < (int)gas.size(); i++) {
        int diff = gas[i] - cost[i];
        current_sum += diff;
        total_sum += diff;
        if (current_sum < 0) {
            start = i + 1;
            current_sum = 0;
        }
    }
    if (total_sum >= 0) return start;
    return -1;
}
```

### Rust

```rust
fn can_complete_circuit(gas: &[i32], cost: &[i32]) -> i32 {
    let mut start: i32 = 0;
    let mut total_sum: i32 = 0;
    let mut current_sum: i32 = 0;
    for i in 0..gas.len() {
        let diff = gas[i] - cost[i];
        current_sum += diff;
        total_sum += diff;
        if current_sum < 0 {
            start = i as i32 + 1;
            current_sum = 0;
        }
    }
    if total_sum >= 0 {
        start
    } else {
        -1
    }
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/gas-station.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
