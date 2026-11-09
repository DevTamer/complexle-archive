# Add Two Numbers

**Puzzle date:** 2026-11-08  
**Category:** linked list  
**Time complexity:** `O(n + m)`  
**Space complexity:** `O(n + m)`

## Explanation

The loop advances through both lists at once and stops when both are exhausted, doing constant-time addition and node creation at each step, so the work is proportional to the length of the longer list and is bounded by n + m. There is no nesting and no re-traversal, so O(n * m) is the wrong instinct. Space is O(n + m) because a brand-new linked list is built to hold the sum: it has as many nodes as the longer input, plus possibly one more for a final carry. The inputs themselves are only walked, never copied.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class ListNode:
    def __init__(self, val: int = 0, next: 'ListNode | None' = None):
        self.val = val
        self.next = next


def add_two_numbers(l1: ListNode | None, l2: ListNode | None) -> ListNode | None:
    dummy = ListNode(0)
    current = dummy
    carry = 0

    while l1 or l2:
        val = carry
        if l1:
            val += l1.val
            l1 = l1.next
        if l2:
            val += l2.val
            l2 = l2.next
        carry, val = divmod(val, 10)
        current.next = ListNode(val)
        current = current.next

    if carry == 1:
        current.next = ListNode(1)

    return dummy.next
```

### C++

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode dummy(0);
    ListNode* current = &dummy;
    int carry = 0;

    while (l1 || l2) {
        int val = carry;
        if (l1) { val += l1->val; l1 = l1->next; }
        if (l2) { val += l2->val; l2 = l2->next; }
        carry = val / 10;
        val = val % 10;
        current->next = new ListNode(val);
        current = current->next;
    }

    if (carry == 1) {
        current->next = new ListNode(1);
    }

    return dummy.next;
}
```

### Rust

```rust
#[derive(Debug)]
struct ListNode {
    val: i32,
    next: Option<Box<ListNode>>,
}

impl ListNode {
    fn new(val: i32) -> Self {
        ListNode { val, next: None }
    }
}

fn add_two_numbers(l1: Option<Box<ListNode>>, l2: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
    let mut dummy = Box::new(ListNode::new(0));
    let mut current = &mut dummy;
    let mut carry = 0;
    let mut l1 = l1;
    let mut l2 = l2;

    while l1.is_some() || l2.is_some() {
        let mut val = carry;
        if let Some(n) = l1 {
            val += n.val;
            l1 = n.next;
        }
        if let Some(n) = l2 {
            val += n.val;
            l2 = n.next;
        }
        carry = val / 10;
        val = val % 10;
        current.next = Some(Box::new(ListNode::new(val)));
        current = current.next.as_mut().unwrap();
    }

    if carry == 1 {
        current.next = Some(Box::new(ListNode::new(1)));
    }

    dummy.next
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/add-two-numbers.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
