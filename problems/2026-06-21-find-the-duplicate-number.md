# Find the Duplicate Number

**Puzzle date:** 2026-06-21  
**Category:** cycle detection  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost here is the two-pointer (Floyd's cycle detection) traversal through the array, which drives both loops. In the first loop, the slow and fast pointers move through the array following index links — the fast pointer moves at most 2n steps before the two meet, so this is O(n). In the second loop, both pointers move one step at a time until they converge on the duplicate, again taking at most O(n) steps. You might be tempted to say O(n²) because there are two separate while loops, but they run sequentially — not nested — so their costs add rather than multiply, keeping the total linear. For space, you only use two integer variables (slow and fast) regardless of the input size, so no extra memory is allocated proportional to n, giving O(1) space.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def find_duplicate(nums: list[int]) -> int:
    slow = fast = nums[0]
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast:
            break
    slow = nums[0]
    while slow != fast:
        slow = nums[slow]
        fast = nums[fast]
    return slow
```

### C++

```cpp
int findDuplicate(std::vector<int>& nums) {
    int slow = nums[0], fast = nums[0];
    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while (slow != fast);
    slow = nums[0];
    while (slow != fast) {
        slow = nums[slow];
        fast = nums[fast];
    }
    return slow;
}
```

### Rust

```rust
fn find_duplicate(nums: &[i32]) -> i32 {
    let mut slow = nums[0] as usize;
    let mut fast = nums[0] as usize;
    loop {
        slow = nums[slow] as usize;
        fast = nums[nums[fast] as usize] as usize;
        if slow == fast { break; }
    }
    slow = nums[0] as usize;
    while slow != fast {
        slow = nums[slow] as usize;
        fast = nums[fast] as usize;
    }
    slow as i32
}
```

---

Played daily at [complexle.com](https://complexle.com).
