# Reverse Linked List

**Puzzle date:** 2026-06-16  
**Category:** linked list  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the single while loop in reverse_list, which visits every node in the linked list exactly once. Since the list has n nodes, the loop runs n times, giving you O(n) time. The most tempting wrong time answer is O(n²), but there is no nested loop or repeated traversal — each node is touched exactly once and then moved on from. For space, you only ever use three pointer variables (prev, curr, nxt) regardless of how long the list is, so the extra memory stays constant at O(1). You might be tempted to say O(n) for space if you think about the list itself, but the algorithm works in-place and does not allocate any new nodes or data structures that grow with input size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def reverse_list(head: ListNode | None) -> ListNode | None:
    prev, curr = None, head
    while curr:
        nxt = curr.next
        curr.next = prev
        prev = curr
        curr = nxt
    return prev
```

### C++

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* reverseList(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* curr = head;
    while (curr) {
        ListNode* nxt = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nxt;
    }
    return prev;
}
```

### Rust

```rust
struct ListNode {
    val: i32,
    next: Option<Box<ListNode>>,
}

fn reverse_list(mut head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
    let mut prev = None;
    while let Some(mut curr) = head {
        head = curr.next.take();
        curr.next = prev;
        prev = Some(curr);
    }
    prev
}
```

---

Played daily at [complexle.com](https://complexle.com).
