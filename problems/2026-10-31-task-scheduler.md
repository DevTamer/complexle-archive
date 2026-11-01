# Task Scheduler

**Puzzle date:** 2026-10-31  
**Category:** heap  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

Counter walks the task list once, max scans the counts once, and list(...).count(...) scans them again — three linear passes, with the final arithmetic being constant time, so the whole function is O(n). There is no sorting and no heap here despite the greedy scheduling flavour of the problem, so O(n log n) is the natural but incorrect guess. Space is O(n) because the Counter holds one entry per distinct task and list(counter.values()) materialises those counts into a new list; in the worst case every task is distinct and both structures hold n elements.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def least_interval(tasks: list[str], n: int) -> int:
    counter = Counter(tasks)
    max_count = max(counter.values())
    num_max = list(counter.values()).count(max_count)
    return max((max_count - 1) * (n + 1) + num_max, len(tasks))
```

### C++

```cpp
int leastInterval(std::vector<char>& tasks, int n) {
    std::unordered_map<char, int> count;
    int max_count = 0;
    for (const auto& task : tasks) {
        ++count[task];
        max_count = std::max(max_count, count[task]);
    }
    int result = (max_count - 1) * (n + 1);
    for (const auto& kvp : count) {
        if (kvp.second == max_count) {
            ++result;
        }
    }
    return std::max(result, static_cast<int>(tasks.size()));
}
```

### Rust

```rust
fn least_interval(tasks: &[char], n: i32) -> i32 {
    let mut count: HashMap<char, i32> = HashMap::new();
    let mut max_count = 0;
    for &task in tasks {
        let c = count.entry(task).or_insert(0);
        *c += 1;
        if *c > max_count {
            max_count = *c;
        }
    }
    let mut result = (max_count - 1) * (n + 1);
    for (_, &v) in count.iter() {
        if v == max_count {
            result += 1;
        }
    }
    std::cmp::max(result, tasks.len() as i32)
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/task-scheduler.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
