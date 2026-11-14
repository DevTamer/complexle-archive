# Add Two Numbers II

**Puzzle date:** 2026-11-13  
**Category:** linked list  
**Time complexity:** `O(n + m)`  
**Space complexity:** `O(n + m)`

## Explanation

Two passes copy the lists into stacks, and a third loop pops them together while building the result, so every node is touched a constant number of times for O(n + m) total. Space is also O(n + m), and here it is unavoidable rather than incidental: the digits must be added from least significant to most, but a singly linked list can only be walked forwards, so both lists are materialised into stacks to reverse them. Those two stacks hold n and m values respectively, and the freshly built result list adds more on top.

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
    stk1: list[int] = []
    stk2: list[int] = []
    while l1:
        stk1.append(l1.val)
        l1 = l1.next
    while l2:
        stk2.append(l2.val)
        l2 = l2.next

    prev: ListNode | None = None
    head: ListNode | None = None
    total = 0
    while stk1 or stk2:
        total //= 10
        if stk1:
            total += stk1.pop()
        if stk2:
            total += stk2.pop()

        head = ListNode(total % 10)
        head.next = prev
        prev = head

    if total >= 10:
        head = ListNode(total // 10)
        head.next = prev

    return head
```

### C++

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    std::stack<int> stk1, stk2;
    while (l1) {
        stk1.push(l1->val);
        l1 = l1->next;
    }
    while (l2) {
        stk2.push(l2->val);
        l2 = l2->next;
    }

    ListNode *prev = nullptr, *head = nullptr;
    int total = 0;
    while (!stk1.empty() || !stk2.empty()) {
        total /= 10;
        if (!stk1.empty()) {
            total += stk1.top();
            stk1.pop();
        }
        if (!stk2.empty()) {
            total += stk2.top();
            stk2.pop();
        }

        head = new ListNode(total % 10);
        head->next = prev;
        prev = head;
    }

    if (total >= 10) {
        head = new ListNode(total / 10);
        head->next = prev;
    }

    return head;
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
    let mut stk1: Vec<i32> = Vec::new();
    let mut stk2: Vec<i32> = Vec::new();

    let mut node = l1;
    while let Some(n) = node {
        stk1.push(n.val);
        node = n.next;
    }
    let mut node = l2;
    while let Some(n) = node {
        stk2.push(n.val);
        node = n.next;
    }

    let mut prev: Option<Box<ListNode>> = None;
    let mut total: i32 = 0;
    while !stk1.is_empty() || !stk2.is_empty() {
        total /= 10;
        if let Some(v) = stk1.pop() {
            total += v;
        }
        if let Some(v) = stk2.pop() {
            total += v;
        }

        let mut head = Box::new(ListNode::new(total % 10));
        head.next = prev;
        prev = Some(head);
    }

    if total >= 10 {
        let mut head = Box::new(ListNode::new(total / 10));
        head.next = prev;
        prev = Some(head);
    }

    prev
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/add-two-numbers-ii.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
