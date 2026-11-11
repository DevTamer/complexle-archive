# Odd Even Linked List

**Puzzle date:** 2026-11-10  
**Category:** linked list  
**Time complexity:** `O(n)`  
**Space complexity:** `O(1)`

## Explanation

The while loop advances cur by one node per iteration and every step does a fixed amount of pointer rewiring, so each node is handled exactly once for O(n) overall. The space is the interesting half: no new nodes are allocated and no list or stack is built — the function relinks the existing nodes in place using a handful of pointer variables, so the extra space is O(1). Answering O(n) is the common mistake, from assuming the odd and even groups must be collected into separate lists before being joined.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class ListNode:
    def __init__(self, val: int = 0, next: Optional["ListNode"] = None):
        self.val = val
        self.next = next

def odd_even_list(head: Optional[ListNode]) -> Optional[ListNode]:
    if head:
        odd_tail, cur = head, head.next
        while cur and cur.next:
            even_head = odd_tail.next
            odd_tail.next = cur.next
            odd_tail = odd_tail.next
            cur.next = odd_tail.next
            odd_tail.next = even_head
            cur = cur.next
    return head
```

### C++

```cpp
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* oddEvenList(ListNode* head) {
    if (head) {
        for (auto odd_tail = head, curr = head->next;
             curr && curr->next;
             curr = curr->next) {
            ListNode *even_head = odd_tail->next;
            odd_tail->next = curr->next;
            odd_tail = odd_tail->next;
            curr->next = odd_tail->next;
            odd_tail->next = even_head;
        }
    }
    return head;
}
```

### Rust

```rust
#[derive(Debug, PartialEq, Eq)]
struct ListNode {
    val: i32,
    next: Option<Box<ListNode>>,
}

impl ListNode {
    fn new(val: i32) -> Self {
        ListNode { val, next: None }
    }
}

fn odd_even_list(mut head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
    if head.is_none() {
        return head;
    }
    let mut odd_tail: &mut Option<Box<ListNode>> = &mut head;
    let mut even_head = odd_tail.as_mut().unwrap().next.take();
    let mut even_tail: &mut Option<Box<ListNode>> = &mut even_head;

    loop {
        if even_tail.is_none() {
            break;
        }
        let next_odd = even_tail.as_mut().unwrap().next.take();
        if next_odd.is_none() {
            break;
        }
        let mut next_odd = next_odd;
        let next_even = next_odd.as_mut().unwrap().next.take();
        odd_tail.as_mut().unwrap().next = next_odd;
        odd_tail = &mut odd_tail.as_mut().unwrap().next;
        even_tail.as_mut().unwrap().next = next_even;
        even_tail = &mut even_tail.as_mut().unwrap().next;
    }

    odd_tail.as_mut().unwrap().next = even_head;
    head
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/odd-even-linked-list.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
