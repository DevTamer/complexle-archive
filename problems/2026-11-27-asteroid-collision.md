# Asteroid Collision

**Puzzle date:** 2026-11-27  
**Category:** stack  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the single pass over the asteroids, plus the inner while loop that pops from the result stack. Each asteroid is pushed onto the stack at most once and popped at most once, so across the whole run the pops can never total more than n. That makes the total work proportional to n. The tempting answer is O(n²) because a while loop sits inside a for loop, but the inner loop's work is shared across all iterations rather than repeated, so it averages out to constant time per asteroid. Space is O(n) because the result stack can hold every asteroid, for example when they all move right.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def asteroid_collision(asteroids: list[int]) -> list[int]:
    result = []
    for x in asteroids:
        if x > 0:
            result.append(x)
            continue
        while result and 0 < result[-1] < -x:
            result.pop()
        if result and 0 < result[-1]:
            if result[-1] == -x:
                result.pop()
            continue
        result.append(x)
    return result
```

### C++

```cpp
std::vector<int> asteroidCollision(std::vector<int>& asteroids) {
    std::vector<int> result;
    for (int x : asteroids) {
        if (x > 0) {
            result.push_back(x);
            continue;
        }
        while (!result.empty() && 0 < result.back() && result.back() < -x) {
            result.pop_back();
        }
        if (!result.empty() && 0 < result.back()) {
            if (result.back() == -x)
                result.pop_back();
            continue;
        }
        result.push_back(x);
    }
    return result;
}
```

### Rust

```rust
fn asteroid_collision(asteroids: &[i32]) -> Vec<i32> {
    let mut result: Vec<i32> = Vec::new();
    for &x in asteroids {
        if x > 0 {
            result.push(x);
            continue;
        }
        while let Some(&top) = result.last() {
            if 0 < top && top < -x {
                result.pop();
            } else {
                break;
            }
        }
        if let Some(&top) = result.last() {
            if top > 0 {
                if top == -x {
                    result.pop();
                }
                continue;
            }
        }
        result.push(x);
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/asteroid-collision.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
