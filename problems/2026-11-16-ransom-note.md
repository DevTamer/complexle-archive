# Ransom Note

**Puzzle date:** 2026-11-16  
**Category:** hash map  
**Time complexity:** `O(n + m)`  
**Space complexity:** `O(1)`

## Explanation

Each string is scanned once with constant-time array indexing per character, so the time is proportional to the two lengths added together; the early break can stop the second loop sooner but does not change the worst case. The space is the point of the puzzle: counts is a fixed array of 26 slots, one per lowercase letter, and its size never depends on how long the inputs are. Extra space is therefore O(1), even though a list is allocated — a frequency structure is only O(n) when it can grow with the input, as a dictionary would.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def can_construct(ransom_note: str, magazine: str) -> bool:
    counts = [0] * 26
    letters = 0

    for c in ransom_note:
        idx = ord(c) - ord('a')
        if counts[idx] == 0:
            letters += 1
        counts[idx] += 1

    for c in magazine:
        idx = ord(c) - ord('a')
        counts[idx] -= 1
        if counts[idx] == 0:
            letters -= 1
            if letters == 0:
                break

    return letters == 0
```

### C++

```cpp
bool canConstruct(std::string ransomNote, std::string magazine) {
    std::vector<int> counts(26, 0);
    int letters = 0;
    for (char c : ransomNote) {
        if (counts[c - 'a']++ == 0) {
            ++letters;
        }
    }
    for (char c : magazine) {
        if (--counts[c - 'a'] == 0 && --letters == 0) {
            break;
        }
    }
    return letters == 0;
}
```

### Rust

```rust
fn can_construct(ransom_note: &str, magazine: &str) -> bool {
    let mut counts = [0i32; 26];
    let mut letters = 0;

    for c in ransom_note.bytes() {
        let idx = (c - b'a') as usize;
        if counts[idx] == 0 {
            letters += 1;
        }
        counts[idx] += 1;
    }

    for c in magazine.bytes() {
        let idx = (c - b'a') as usize;
        counts[idx] -= 1;
        if counts[idx] == 0 {
            letters -= 1;
            if letters == 0 {
                break;
            }
        }
    }

    letters == 0
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/ransom-note.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
