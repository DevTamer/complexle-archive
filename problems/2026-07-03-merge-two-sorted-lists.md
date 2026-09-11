# Merge Two Sorted Lists

**Puzzle date:** 2026-07-03  
**Category:** linked list  
**Time complexity:** `O(n + m)`  
**Space complexity:** `O(1)`

## Explanation

The dominant cost is the while loop, which advances through both lists one node at a time. Each iteration moves either l1 or l2 forward by one step, so in the worst case you visit every node in both lists — that's O(n + m) where n and m are the lengths of l1 and l2 respectively. After the loop, the remaining tail is attached in O(1) with 'curr.next = l1 or l2'. The most tempting wrong time answer is O(min(n, m)) because the while loop stops when either list is exhausted, but the remaining nodes are still 'processed' via the tail assignment, meaning all nodes are effectively touched. For space, you only allocate a single dummy node and a curr pointer regardless of input size, so no extra space grows with the input — the merged list reuses the existing nodes, making it O(1) auxiliary space.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def merge_two_lists(l1: ListNode | None, l2: ListNode | None) -> ListNode | None:
    dummy = curr = ListNode()
    while l1 and l2:
        if l1.val <= l2.val:
            curr.next, l1 = l1, l1.next
        else:
            curr.next, l2 = l2, l2.next
        curr = curr.next
    curr.next = l1 or l2
    return dummy.next
```

### C++

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode dummy(0);
    ListNode* curr = &dummy;
    while (l1 && l2) {
        if (l1->val <= l2->val) {
            curr->next = l1;
            l1 = l1->next;
        } else {
            curr->next = l2;
            l2 = l2->next;
        }
        curr = curr->next;
    }
    curr->next = l1 ? l1 : l2;
    return dummy.next;
}
```

### Rust

```rust
struct ListNode {
    val: i32,
    next: Option<Box<ListNode>>,
}

fn merge_two_lists(
    mut l1: Option<Box<ListNode>>,
    mut l2: Option<Box<ListNode>>,
) -> Option<Box<ListNode>> {
    let mut dummy = Box::new(ListNode { val: 0, next: None });
    let mut curr = &mut dummy;
    while l1.is_some() && l2.is_some() {
        if l1.as_ref().unwrap().val <= l2.as_ref().unwrap().val {
            let mut n = l1.take().unwrap();
            l1 = n.next.take();
            curr.next = Some(n);
        } else {
            let mut n = l2.take().unwrap();
            l2 = n.next.take();
            curr.next = Some(n);
        }
        curr = curr.next.as_mut().unwrap();
    }
    curr.next = l1.or(l2);
    dummy.next
}
```

---

Played daily at [complexle.com](https://complexle.com).
