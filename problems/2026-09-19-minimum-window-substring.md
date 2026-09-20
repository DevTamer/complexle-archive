# Minimum Window Substring

**Puzzle date:** 2026-09-19  
**Category:** sliding window  
**Time complexity:** `O(n + m)`  
**Space complexity:** `O(m)`

## Explanation

You have two pointers, i and j, that each move forward through the string s, and the inner while loop's total iterations across the whole run are bounded by n because i never resets or moves backward, so the sliding window scan is O(n), plus O(m) to build the Counter from t. It's tempting to think the while loop nested inside the for loop makes this O(n^2), but that's wrong because i only increases and never exceeds j, so combined the two pointers do at most 2n steps total, not n*m or n^2. The space cost comes from the Counter dictionary, which stores at most one entry per distinct character in t, giving O(m) where m is the length of t (or O(1) if you assume a fixed alphabet like ASCII). Since count is built from t and only ever tracks characters from t, it doesn't grow with the size of s, so space isn't O(n) or O(n+m).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def min_window(s: str, t: str) -> str:
    count = collections.Counter(t)
    remain = len(t)
    i, left, right = 0, -1, -1
    for j, c in enumerate(s):
        remain -= count[c] > 0
        count[c] -= 1
        if remain:
            continue
        while count[s[i]] < 0:
            count[s[i]] += 1
            i += 1
        if right == -1 or j - i + 1 < right - left + 1:
            left, right = i, j
    return s[left:right + 1]
```

### C++

```cpp
std::string minWindow(std::string s, std::string t) {
    std::unordered_map<char, int> count;
    for (char c : t) count[c]++;
    int remain = (int)t.size();
    int left = -1, right = -1;
    for (int i = 0, j = 0; j < (int)s.size(); ++j) {
        remain -= count[s[j]]-- > 0;
        if (remain) continue;
        while (count[s[i]] < 0) {
            ++count[s[i]];
            ++i;
        }
        if (right == -1 || j - i + 1 < right - left + 1) {
            left = i;
            right = j;
        }
    }
    return left >= 0 ? s.substr(left, right - left + 1) : "";
}
```

### Rust

```rust
fn min_window(s: &str, t: &str) -> String {
    let s_bytes = s.as_bytes();
    let mut count: HashMap<u8, i32> = HashMap::new();
    for b in t.bytes() {
        *count.entry(b).or_insert(0) += 1;
    }
    let mut remain = t.len() as i32;
    let mut i: usize = 0;
    let mut left: i32 = -1;
    let mut right: i32 = -1;
    for j in 0..s_bytes.len() {
        let c = s_bytes[j];
        let cnt = count.entry(c).or_insert(0);
        let was_positive = *cnt > 0;
        if was_positive {
            remain -= 1;
        }
        *cnt -= 1;
        if remain > 0 {
            continue;
        }
        while *count.get(&s_bytes[i]).unwrap() < 0 {
            *count.get_mut(&s_bytes[i]).unwrap() += 1;
            i += 1;
        }
        if right == -1 || (j as i32 - i as i32 + 1) < (right - left + 1) {
            left = i as i32;
            right = j as i32;
        }
    }
    if left == -1 {
        String::new()
    } else {
        String::from_utf8(s_bytes[left as usize..(right as usize + 1)].to_vec()).unwrap()
    }
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/minimum-window-substring.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
