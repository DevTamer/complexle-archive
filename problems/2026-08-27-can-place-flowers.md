# Can Place Flowers

**Puzzle date:** 2026-08-27  
**Category:** arrays  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The single for loop iterates once over the flowerbed array, checking each position for a valid planting spot, so the dominant cost is that one pass through the list of length n. Each check inside the loop (comparing neighbors) is constant time, so the total work scales linearly with the size of the input array. You might be tempted to say O(1) because the function can return early once n reaches zero, but early exits only improve the best case, not the worst-case bound, which still requires scanning up to all n elements. The space complexity is O(n) because the code makes a full copy of the flowerbed list with 'bed = flowerbed[:]' rather than modifying the input in place, so extra memory proportional to the input size is allocated.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def can_place_flowers(flowerbed: list[int], n: int) -> bool:
    bed = flowerbed[:]
    for i in range(len(bed)):
        if bed[i] == 0 and (i == 0 or bed[i - 1] == 0) and \
           (i == len(bed) - 1 or bed[i + 1] == 0):
            bed[i] = 1
            n -= 1
        if n <= 0:
            return True
    return False
```

### C++

```cpp
bool canPlaceFlowers(std::vector<int>& flowerbed, int n) {
    for (size_t i = 0; i < flowerbed.size(); ++i) {
        if (flowerbed[i] == 0 && (i == 0 || flowerbed[i - 1] == 0) &&
            (i == flowerbed.size() - 1 || flowerbed[i + 1] == 0)) {
            flowerbed[i] = 1;
            --n;
        }
        if (n <= 0) {
            return true;
        }
    }
    return false;
}
```

### Rust

```rust
fn can_place_flowers(flowerbed: &[i32], n: i32) -> bool {
    let mut bed = flowerbed.to_vec();
    let mut n = n;
    for i in 0..bed.len() {
        if bed[i] == 0 && (i == 0 || bed[i - 1] == 0) &&
           (i == bed.len() - 1 || bed[i + 1] == 0) {
            bed[i] = 1;
            n -= 1;
        }
        if n <= 0 {
            return true;
        }
    }
    false
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/can-place-flowers.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
