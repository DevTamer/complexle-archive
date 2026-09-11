# Linked List Cycle

**Puzzle date:** 2026-07-04  
**Category:** cycle detection  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the while loop, which advances two pointers (slow and fast) through the linked list. If there is no cycle, the fast pointer reaches the end in at most n/2 iterations, which simplifies to O(n). If there is a cycle, the fast pointer laps the slow pointer within at most n steps, so the loop still runs O(n) times total. You might be tempted to say O(n²) thinking the two pointers create nested work, but both pointers move forward in a single loop — there is no nested iteration, just two references advancing in tandem. The space complexity is O(1) because you only use two pointer variables (slow and fast) regardless of the size of the list — no extra data structure grows with input.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def has_cycle(head: ListNode | None) -> bool:
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow is fast:
            return True
    return False
```

### C++

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

bool hasCycle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) return true;
    }
    return false;
}
```

### Rust

```rust
use std::cell::RefCell;
use std::rc::Rc;

struct ListNode {
    val: i32,
    next: Option<Rc<RefCell<ListNode>>>,
}

fn has_cycle(head: Option<Rc<RefCell<ListNode>>>) -> bool {
    let mut slow = head.clone();
    let mut fast = head;
    loop {
        fast = match fast {
            Some(node) => node.borrow().next.clone(),
            None => return false,
        };
        fast = match fast {
            Some(node) => node.borrow().next.clone(),
            None => return false,
        };
        slow = match slow {
            Some(node) => node.borrow().next.clone(),
            None => return false,
        };
        if let (Some(s), Some(f)) = (&slow, &fast) {
            if Rc::ptr_eq(s, f) {
                return true;
            }
        }
    }
}
```

---

Played daily at [complexle.com](https://complexle.com).
