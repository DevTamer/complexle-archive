# Group Anagrams

**Puzzle date:** 2026-06-23  
**Category:** hash map  
**Time complexity:** `O(n * k)`  
**Space complexity:** `O(n * k)`

## Explanation

The dominant cost is the outer loop over all n strings, and for each string, the inner loop over its characters of length k, making the total time O(n * k). The key insight is that building the frequency count array takes O(k) per string, and converting it to a tuple also takes O(26) which is constant, so the character counting drives the cost. You might be tempted to say O(n * k * log k) thinking that sorting each string is required — but this solution cleverly avoids sorting by using a fixed-size 26-element count array as the key instead. For space, you store every original string in the hash map and each key is a tuple of 26 integers, so across all n strings of average length k the total storage is O(n * k) for the strings themselves, which dominates the O(26n) key storage.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def group_anagrams(strs: list[str]) -> list[list[str]]:
    groups = defaultdict(list)
    for s in strs:
        key = [0] * 26
        for ch in s:
            key[ord(ch) - ord('a')] += 1
        groups[tuple(key)].append(s)
    return list(groups.values())
```

### C++

```cpp
std::vector<std::vector<std::string>> groupAnagrams(std::vector<std::string>& strs) {
    std::unordered_map<std::string, std::vector<std::string>> groups;
    for (const auto& s : strs) {
        std::string key(26, '0');
        for (char c : s) key[c - 'a']++;
        groups[key].push_back(s);
    }
    std::vector<std::vector<std::string>> result;
    for (auto& [_, v] : groups) result.push_back(std::move(v));
    return result;
}
```

### Rust

```rust
fn group_anagrams(strs: Vec<String>) -> Vec<Vec<String>> {
    let mut groups: HashMap<[u8; 26], Vec<String>> = HashMap::new();
    for s in strs {
        let mut key = [0u8; 26];
        for b in s.bytes() {
            key[(b - b'a') as usize] += 1;
        }
        groups.entry(key).or_default().push(s);
    }
    groups.into_values().collect()
}
```

---

Played daily at [complexle.com](https://complexle.com).
