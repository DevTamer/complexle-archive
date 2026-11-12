# Binary Tree Zigzag Level Order Traversal

**Puzzle date:** 2026-11-11  
**Category:** tree  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

This is a level-order traversal: every node is appended to exactly one level list and visited exactly once, so the traversal is O(n). The reversal on alternating levels looks like extra cost, but reversing a level of size k is O(k) and the level sizes sum to n across the whole tree, so the reversals add O(n) in total rather than multiplying anything. Space is O(n): the result holds every value, and the current and next_level lists can together hold an entire level, which for the bottom level of a balanced tree is about half the nodes.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class TreeNode:
    def __init__(self, val: int = 0, left: "TreeNode | None" = None, right: "TreeNode | None" = None):
        self.val = val
        self.left = left
        self.right = right


def zigzag_level_order(root: "TreeNode | None") -> list[list[int]]:
    if root is None:
        return []
    result, current = [], [root]
    while current:
        next_level, vals = [], []
        for node in current:
            vals.append(node.val)
            if node.left:
                next_level.append(node.left)
            if node.right:
                next_level.append(node.right)
        result.append(vals[::-1] if len(result) % 2 else vals)
        current = next_level
    return result
```

### C++

```cpp
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

std::vector<std::vector<int>> zigzagLevelOrder(TreeNode* root) {
    std::vector<std::vector<int>> result;
    if (root == nullptr) return result;
    std::vector<TreeNode*> current = {root};
    while (!current.empty()) {
        std::vector<TreeNode*> nextLevel;
        std::vector<int> vals;
        for (TreeNode* node : current) {
            vals.push_back(node->val);
            if (node->left) nextLevel.push_back(node->left);
            if (node->right) nextLevel.push_back(node->right);
        }
        if (result.size() % 2 == 1) {
            std::reverse(vals.begin(), vals.end());
        }
        result.push_back(vals);
        current = nextLevel;
    }
    return result;
}
```

### Rust

```rust
#[derive(Debug)]
struct TreeNode {
    val: i32,
    left: Option<Rc<RefCell<TreeNode>>>,
    right: Option<Rc<RefCell<TreeNode>>>,
}

impl TreeNode {
    fn new(val: i32) -> Self {
        TreeNode { val, left: None, right: None }
    }
}

fn zigzag_level_order(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<Vec<i32>> {
    let mut result: Vec<Vec<i32>> = Vec::new();
    let mut current: Vec<Rc<RefCell<TreeNode>>> = match root {
        Some(node) => vec![node],
        None => return result,
    };
    while !current.is_empty() {
        let mut next_level: Vec<Rc<RefCell<TreeNode>>> = Vec::new();
        let mut vals: Vec<i32> = Vec::new();
        for node in &current {
            let node_ref = node.borrow();
            vals.push(node_ref.val);
            if let Some(left) = &node_ref.left {
                next_level.push(Rc::clone(left));
            }
            if let Some(right) = &node_ref.right {
                next_level.push(Rc::clone(right));
            }
        }
        if result.len() % 2 == 1 {
            vals.reverse();
        }
        result.push(vals);
        current = next_level;
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/binary-tree-zigzag-level-order-traversal.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
