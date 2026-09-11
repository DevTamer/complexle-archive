# Majority Element II

**Puzzle date:** 2026-08-31  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost comes from the two separate passes over the nums list, each of which is O(n), plus a small inner loop over the keys of cnts. That inner loop looks like it could add extra cost, but the algorithm's logic (the Boyer-Moore style k=3 majority vote) guarantees cnts never holds more than k-1, i.e. 2, keys at any time, since the moment a third key would be added, every counter gets decremented and empties out. So that inner loop is bounded by a constant, not by n, and the overall time stays O(n). A tempting wrong answer is O(n^2), assuming the inner 'for j in list(cnts.keys())' loop scales with the outer loop, but since cnts is capped at a fixed small size regardless of n, it contributes only a constant factor. Space is O(1) because the dictionary size stays bounded by k (a fixed constant of 3) throughout the algorithm, independent of how large nums grows, and the final result list also holds at most k-1 elements.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def majority_element(nums: list[int]) -> list[int]:
    k = 3
    n = len(nums)
    cnts: dict[int, int] = {}

    for i in nums:
        cnts[i] = cnts.get(i, 0) + 1
        if len(cnts) == k:
            for j in list(cnts.keys()):
                cnts[j] -= 1
                if cnts[j] == 0:
                    del cnts[j]

    for i in cnts.keys():
        cnts[i] = 0

    for i in nums:
        if i in cnts:
            cnts[i] += 1

    result = [i for i in cnts.keys() if cnts[i] > n / k]
    return sorted(result)
```

### C++

```cpp
#include <vector>
#include <unordered_map>
#include <algorithm>

std::vector<int> majorityElement(std::vector<int>& nums) {
    int k = 3;
    int n = nums.size();
    std::unordered_map<int, int> hash;

    for (int i : nums) {
        hash[i]++;
        if ((int)hash.size() == k) {
            for (auto it = hash.begin(); it != hash.end(); ) {
                if (--(it->second) == 0) {
                    it = hash.erase(it);
                } else {
                    ++it;
                }
            }
        }
    }

    for (auto& it : hash) {
        it.second = 0;
    }

    for (int i : nums) {
        auto it = hash.find(i);
        if (it != hash.end()) {
            it->second++;
        }
    }

    std::vector<int> ret;
    for (auto& it : hash) {
        if (it.second > n / k) {
            ret.push_back(it.first);
        }
    }
    std::sort(ret.begin(), ret.end());
    return ret;
}
```

### Rust

```rust
use std::collections::HashMap;

fn majority_element(nums: &[i32]) -> Vec<i32> {
    let k = 3usize;
    let n = nums.len();
    let mut cnts: HashMap<i32, i32> = HashMap::new();

    for &i in nums {
        *cnts.entry(i).or_insert(0) += 1;
        if cnts.len() == k {
            let keys: Vec<i32> = cnts.keys().cloned().collect();
            for j in keys {
                if let Some(val) = cnts.get_mut(&j) {
                    *val -= 1;
                    if *val == 0 {
                        cnts.remove(&j);
                    }
                }
            }
        }
    }

    for val in cnts.values_mut() {
        *val = 0;
    }

    for &i in nums {
        if let Some(val) = cnts.get_mut(&i) {
            *val += 1;
        }
    }

    let mut result: Vec<i32> = cnts
        .into_iter()
        .filter(|&(_, v)| (v as usize) > n / k)
        .map(|(key, _)| key)
        .collect();
    result.sort();
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/majority-element-ii.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
