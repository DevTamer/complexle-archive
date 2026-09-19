# Fruit Into Baskets

**Puzzle date:** 2026-09-18  
**Category:** sliding window  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here comes from the two pointers i and j moving through the tree list. Even though there's a while loop nested inside the for loop, you should notice that i only ever increases and never resets, so across the whole run it can advance at most n times total, not n times per outer iteration. That means the combined work of the for loop and the while loop is still bounded by O(n), not O(n^2), which is the most tempting wrong answer since nested loops often signal quadratic time. For space, the count dictionary is capped at holding at most 3 distinct fruit types at any moment (since the while loop shrinks it back down once it exceeds 2), so it uses constant space regardless of how large the input list gets, giving you O(1) rather than something that grows with n.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def total_fruit(tree: list[int]) -> int:
    count: dict[int, int] = defaultdict(int)
    result, i = 0, 0
    for j, v in enumerate(tree):
        count[v] += 1
        while len(count) > 2:
            count[tree[i]] -= 1
            if count[tree[i]] == 0:
                del count[tree[i]]
            i += 1
        result = max(result, j - i + 1)
    return result
```

### C++

```cpp
int totalFruit(std::vector<int>& tree) {
    std::unordered_map<int, int> count;
    int result = 0;
    for (int i = 0, j = 0; j < (int)tree.size(); ++j) {
        ++count[tree[j]];
        while (count.size() > 2) {
            --count[tree[i]];
            if (count[tree[i]] == 0) {
                count.erase(tree[i]);
            }
            ++i;
        }
        result = std::max(result, j - i + 1);
    }
    return result;
}
```

### Rust

```rust
fn total_fruit(tree: &[i32]) -> i32 {
    let mut count: HashMap<i32, i32> = HashMap::new();
    let mut result: i32 = 0;
    let mut i: usize = 0;
    for j in 0..tree.len() {
        *count.entry(tree[j]).or_insert(0) += 1;
        while count.len() > 2 {
            let c = count.get_mut(&tree[i]).unwrap();
            *c -= 1;
            if *c == 0 {
                count.remove(&tree[i]);
            }
            i += 1;
        }
        result = result.max((j - i + 1) as i32);
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/fruit-into-baskets.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
