# Partition Labels

**Puzzle date:** 2026-09-08  
**Category:** two pointers  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost comes from two separate single passes over the string: one to build the lookup dictionary mapping each character to its last index, and one to scan through and determine partition boundaries. Both loops run exactly n times where n is the length of the string, and all operations inside them (dictionary lookups, max, comparisons) are O(1), so the total time is O(n). You might be tempted to think it's O(n²) because there's a nested-looking structure with 'last' tracking, but there's no actual inner loop scanning back through characters—the max update happens in constant time per character. The space complexity is O(n) because the lookup dictionary can store up to one entry per unique character, which in the worst case (all distinct characters) scales linearly with the input size, plus the result list also grows with input size in the worst case.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def partition_labels(s: str) -> list[int]:
    lookup = {c: i for i, c in enumerate(s)}
    first, last = 0, 0
    result = []
    for i, c in enumerate(s):
        last = max(last, lookup[c])
        if i == last:
            result.append(i - first + 1)
            first = i + 1
    return result
```

### C++

```cpp
std::vector<int> partitionLabels(std::string s) {
    std::unordered_map<char, int> lookup;
    for (int i = 0; i < (int)s.length(); ++i) {
        lookup[s[i]] = i;
    }
    int first = 0, last = 0;
    std::vector<int> result;
    for (int i = 0; i < (int)s.length(); ++i) {
        last = std::max(last, lookup[s[i]]);
        if (i == last) {
            result.push_back(i - first + 1);
            first = i + 1;
        }
    }
    return result;
}
```

### Rust

```rust
fn partition_labels(s: &str) -> Vec<i32> {
    let chars: Vec<char> = s.chars().collect();
    let mut lookup: HashMap<char, usize> = HashMap::new();
    for (i, &c) in chars.iter().enumerate() {
        lookup.insert(c, i);
    }
    let mut first = 0usize;
    let mut last = 0usize;
    let mut result = Vec::new();
    for (i, &c) in chars.iter().enumerate() {
        last = last.max(lookup[&c]);
        if i == last {
            result.push((i - first + 1) as i32);
            first = i + 1;
        }
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/partition-labels.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
