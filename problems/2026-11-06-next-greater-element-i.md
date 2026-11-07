# Next Greater Element I

**Puzzle date:** 2026-11-06  
**Category:** stack  
**Time complexity:** `O(n + m)`  
**Space complexity:** `O(n + m)`

## Explanation

The first loop walks nums with a monotonic stack, where each value is pushed exactly once and popped at most once, so that whole phase is linear in n rather than quadratic despite the inner while. Draining the leftover stack is another O(n), and the final comprehension is one pass over find_nums, giving O(n + m). The tempting answer is O(n * m), which is what a nested search for each query value would cost — the precomputed lookup table is what removes it. Space is O(n + m): the lookup dictionary holds an entry per value in nums, and the returned list holds one per element of find_nums.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def next_greater_element(find_nums: list[int], nums: list[int]) -> list[int]:
    stk = []
    lookup = {}
    for num in nums:
        while stk and num > stk[-1]:
            lookup[stk.pop()] = num
        stk.append(num)
    while stk:
        lookup[stk.pop()] = -1
    return [lookup[x] for x in find_nums]
```

### C++

```cpp
std::vector<int> nextGreaterElement(std::vector<int>& findNums, std::vector<int>& nums) {
    std::stack<int> stk;
    std::unordered_map<int, int> lookup;
    for (const auto& num : nums) {
        while (!stk.empty() && num > stk.top()) {
            lookup[stk.top()] = num;
            stk.pop();
        }
        stk.push(num);
    }
    while (!stk.empty()) {
        lookup[stk.top()] = -1;
        stk.pop();
    }
    std::vector<int> result;
    for (const auto& num : findNums) {
        result.push_back(lookup[num]);
    }
    return result;
}
```

### Rust

```rust
fn next_greater_element(find_nums: &[i32], nums: &[i32]) -> Vec<i32> {
    let mut stk: Vec<i32> = Vec::new();
    let mut lookup: HashMap<i32, i32> = HashMap::new();
    for &num in nums {
        while let Some(&top) = stk.last() {
            if num > top {
                stk.pop();
                lookup.insert(top, num);
            } else {
                break;
            }
        }
        stk.push(num);
    }
    while let Some(top) = stk.pop() {
        lookup.insert(top, -1);
    }
    find_nums.iter().map(|x| lookup[x]).collect()
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/next-greater-element-i.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
