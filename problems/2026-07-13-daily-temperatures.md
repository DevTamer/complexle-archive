# Daily Temperatures

**Puzzle date:** 2026-07-13  
**Category:** stack  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the single for-loop that iterates over all n temperatures, combined with the while-loop that pops from the stack. Although you see a nested while-loop inside the for-loop, each index is pushed onto the stack exactly once and popped at most once, so the total number of stack operations across the entire run is at most 2n — giving you O(n) overall. The most tempting wrong answer is O(n²), because the nested while-loop looks like it could run n times for each of the n iterations, but that would require each element to be popped multiple times, which is impossible since each element is pushed only once. For space, the result array and the stack each hold at most n elements, so space is O(n); O(1) is wrong because the stack can grow up to size n in the worst case (e.g., a strictly decreasing temperature list).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def daily_temperatures(temperatures: list[int]) -> list[int]:
    result = [0] * len(temperatures)
    stack = []
    for i, t in enumerate(temperatures):
        while stack and temperatures[stack[-1]] < t:
            j = stack.pop()
            result[j] = i - j
        stack.append(i)
    return result
```

### C++

```cpp
#include <vector>
#include <stack>

std::vector<int> dailyTemperatures(std::vector<int>& temperatures) {
    std::vector<int> result(temperatures.size(), 0);
    std::stack<int> stk;
    for (int i = 0; i < (int)temperatures.size(); i++) {
        while (!stk.empty() && temperatures[stk.top()] < temperatures[i]) {
            int j = stk.top(); stk.pop();
            result[j] = i - j;
        }
        stk.push(i);
    }
    return result;
}
```

### Rust

```rust
fn daily_temperatures(temperatures: &[i32]) -> Vec<i32> {
    let mut result = vec![0; temperatures.len()];
    let mut stack: Vec<usize> = Vec::new();
    for (i, &t) in temperatures.iter().enumerate() {
        while let Some(&j) = stack.last() {
            if temperatures[j] < t {
                result[j] = (i - j) as i32;
                stack.pop();
            } else {
                break;
            }
        }
        stack.push(i);
    }
    result
}
```

---

Played daily at [complexle.com](https://complexle.com).
