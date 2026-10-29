# First Unique Character in a String

**Puzzle date:** 2026-10-28  
**Category:** hash map  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The for loop makes a single pass over the string, and each iteration does only constant-time work: a dictionary get, plus a set add or discard. The final min(candidates) scans the candidate set once, which is at most n elements, so it adds another O(n) and does not change the overall linear bound. Space is O(n) because both lookup and candidates can grow with the number of distinct characters, which in the worst case — every character unique — is n entries. If the problem were restricted to a fixed alphabet the space would collapse to O(1), but nothing in this code bounds the character set, so it scales with the input.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def first_uniq_char(s: str) -> int:
    lookup: dict[str, int] = {}
    candidates: set[int] = set()
    for i, c in enumerate(s):
        if lookup.get(c):
            candidates.discard(lookup[c])
        else:
            lookup[c] = i + 1
            candidates.add(i + 1)
    return min(candidates) - 1 if candidates else -1
```

### C++

```cpp
int firstUniqChar(const std::string& s) {
    std::unordered_map<char, int> lookup;
    std::unordered_set<int> candidates;
    for (int i = 0; i < (int)s.length(); ++i) {
        char c = s[i];
        if (lookup[c]) {
            candidates.erase(lookup[c]);
        } else {
            lookup[c] = i + 1;
            candidates.insert(i + 1);
        }
    }
    if (candidates.empty()) return -1;
    int m = *candidates.begin();
    for (int v : candidates) {
        if (v < m) m = v;
    }
    return m - 1;
}
```

### Rust

```rust
fn first_uniq_char(s: &str) -> i32 {
    let mut lookup: HashMap<char, i32> = HashMap::new();
    let mut candidates: HashSet<i32> = HashSet::new();
    for (i, c) in s.chars().enumerate() {
        let idx = i as i32 + 1;
        let entry = lookup.entry(c).or_insert(0);
        if *entry != 0 {
            candidates.remove(entry);
        } else {
            *entry = idx;
            candidates.insert(idx);
        }
    }
    match candidates.iter().min() {
        Some(&m) => m - 1,
        None => -1,
    }
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/first-unique-character-in-a-string.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
