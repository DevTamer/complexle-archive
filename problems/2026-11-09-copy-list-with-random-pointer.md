# Copy List with Random Pointer

**Puzzle date:** 2026-11-09  
**Category:** linked list  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The function makes a fixed number of sequential passes over the list — interleaving the copied nodes, wiring up the random pointers, separating the two lists, then indexing and serialising — and each pass visits every node exactly once. A constant number of linear passes is still O(n). The O(n²) instinct comes from imagining a search for each random target, which is exactly what the interleaving trick avoids: each random pointer is resolved in constant time from its neighbour. Space is O(n) because n copied nodes are allocated, plus an index map and result list of the same size.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class Node:
    def __init__(self, val: int = 0):
        self.val = val
        self.next: "Node | None" = None
        self.random: "Node | None" = None


def copy_random_list(values: list[list[int]]) -> list[list[int]]:
    if not values:
        return []
    nodes = [Node(v[0]) for v in values]
    n = len(nodes)
    for i in range(n):
        nodes[i].next = nodes[i + 1] if i + 1 < n else None
        r = values[i][1]
        nodes[i].random = nodes[r] if r >= 0 else None
    head = nodes[0]

    current = head
    while current:
        copied = Node(current.val)
        copied.next = current.next
        current.next = copied
        current = copied.next

    current = head
    while current:
        if current.random:
            current.next.random = current.random.next
        current = current.next.next

    dummy = Node(0)
    copied_current, current = dummy, head
    while current:
        copied_current.next = current.next
        current.next = current.next.next
        copied_current, current = copied_current.next, current.next
    new_head = dummy.next

    index_map = {}
    node = new_head
    i = 0
    while node:
        index_map[id(node)] = i
        node = node.next
        i += 1

    result = []
    node = new_head
    while node:
        r = index_map[id(node.random)] if node.random else -1
        result.append([node.val, r])
        node = node.next
    return result
```

### C++

```cpp
struct Node {
    int val;
    Node* next;
    Node* random;
    Node(int x) : val(x), next(nullptr), random(nullptr) {}
};

std::vector<std::vector<int>> copyRandomList(std::vector<std::vector<int>>& values) {
    if (values.empty()) return {};
    int n = values.size();
    std::vector<Node*> nodes(n);
    for (int i = 0; i < n; i++) nodes[i] = new Node(values[i][0]);
    for (int i = 0; i < n; i++) {
        nodes[i]->next = (i + 1 < n) ? nodes[i + 1] : nullptr;
        int r = values[i][1];
        nodes[i]->random = (r >= 0) ? nodes[r] : nullptr;
    }
    Node* head = nodes[0];

    for (Node* curr = head; curr; curr = curr->next->next) {
        Node* node = new Node(curr->val);
        node->next = curr->next;
        curr->next = node;
    }

    for (Node* curr = head; curr; curr = curr->next->next) {
        if (curr->random) {
            curr->next->random = curr->random->next;
        }
    }

    Node dummy(0);
    Node* copy_curr = &dummy;
    Node* curr = head;
    while (curr) {
        copy_curr->next = curr->next;
        curr->next = curr->next->next;
        copy_curr = copy_curr->next;
        curr = curr->next;
    }
    Node* newHead = dummy.next;

    std::unordered_map<Node*, int> index_map;
    int idx = 0;
    for (Node* node = newHead; node; node = node->next) {
        index_map[node] = idx++;
    }
    std::vector<std::vector<int>> result;
    for (Node* node = newHead; node; node = node->next) {
        int r = node->random ? index_map[node->random] : -1;
        result.push_back({node->val, r});
    }
    return result;
}
```

### Rust

```rust
struct Node {
    val: i32,
    next: Option<Rc<RefCell<Node>>>,
    random: Option<Rc<RefCell<Node>>>,
}

impl Node {
    fn new(val: i32) -> Rc<RefCell<Node>> {
        Rc::new(RefCell::new(Node { val, next: None, random: None }))
    }
}

fn copy_random_list(values: &[Vec<i32>]) -> Vec<Vec<i32>> {
    if values.is_empty() {
        return vec![];
    }
    let n = values.len();
    let nodes: Vec<Rc<RefCell<Node>>> = values.iter().map(|v| Node::new(v[0])).collect();
    for i in 0..n {
        let next = if i + 1 < n { Some(nodes[i + 1].clone()) } else { None };
        nodes[i].borrow_mut().next = next;
        let r = values[i][1];
        let random = if r >= 0 { Some(nodes[r as usize].clone()) } else { None };
        nodes[i].borrow_mut().random = random;
    }
    let head = nodes[0].clone();

    let mut curr = Some(head.clone());
    while let Some(cur) = curr {
        let val = cur.borrow().val;
        let next = cur.borrow().next.clone();
        let copied = Node::new(val);
        copied.borrow_mut().next = next.clone();
        cur.borrow_mut().next = Some(copied);
        curr = next;
    }

    let mut curr = Some(head.clone());
    while let Some(cur) = curr {
        let random = cur.borrow().random.clone();
        let copied = cur.borrow().next.clone().unwrap();
        if let Some(r) = random {
            let r_copy = r.borrow().next.clone();
            copied.borrow_mut().random = r_copy;
        }
        curr = copied.borrow().next.clone();
    }

    let dummy = Node::new(0);
    let mut copy_curr = dummy.clone();
    let mut curr = Some(head.clone());
    while let Some(cur) = curr {
        let copied = cur.borrow().next.clone().unwrap();
        let next_orig = copied.borrow().next.clone();
        copy_curr.borrow_mut().next = Some(copied.clone());
        cur.borrow_mut().next = next_orig.clone();
        copy_curr = copied;
        curr = next_orig;
    }
    let new_head = dummy.borrow().next.clone();

    let mut index_map: HashMap<*const RefCell<Node>, i32> = HashMap::new();
    let mut node = new_head.clone();
    let mut idx = 0;
    while let Some(n) = node {
        index_map.insert(Rc::as_ptr(&n), idx);
        idx += 1;
        node = n.borrow().next.clone();
    }

    let mut result = Vec::new();
    let mut node = new_head;
    while let Some(n) = node {
        let val = n.borrow().val;
        let random = n.borrow().random.clone();
        let r = match random {
            Some(r) => *index_map.get(&Rc::as_ptr(&r)).unwrap(),
            None => -1,
        };
        result.push(vec![val, r]);
        node = n.borrow().next.clone();
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/copy-list-with-random-pointer.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
