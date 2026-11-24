# Middle of the Linked List

**Puzzle date:** 2026-11-23  
**Category:** linked list  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The fast pointer advances two nodes per iteration and the slow pointer one, so the loop ends after about n/2 iterations — still linear in the list length, since constant factors drop out. The two-pointer trick does not beat O(n); what it buys is the space. Because a singly linked list has no length field and no random access, the obvious approach is to walk the list into an array first and index the middle, which costs O(n) memory. Here only two pointer variables are ever held, so the extra space is O(1).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class ListNode:
    def __init__(self, val: int = 0, next: "ListNode | None" = None):
        self.val = val
        self.next = next

def middle_node(head: ListNode | None) -> ListNode | None:
    slow, fast = head, head
    while fast and fast.next:
        slow, fast = slow.next, fast.next.next
    return slow
```

### C++

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* middleNode(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}
```

### Rust

```rust
struct ListNode {
    val: i32,
    next: Option<Box<ListNode>>,
}

impl ListNode {
    fn new(val: i32) -> Self {
        ListNode { val, next: None }
    }
}

fn middle_node(head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
    let mut slow = head.as_deref();
    let mut fast = head.as_deref();
    let mut steps = 0;
    while let Some(f) = fast {
        if let Some(f2) = f.next.as_deref() {
            fast = f2.next.as_deref();
            slow = slow.unwrap().next.as_deref();
            steps += 1;
        } else {
            fast = None;
        }
    }
    let mut cur = head;
    for _ in 0..steps {
        cur = cur.unwrap().next;
    }
    cur
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/middle-of-the-linked-list.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
