# Binary Tree Level Order Traversal

**Puzzle date:** 2026-11-18  
**Category:** tree  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

Every node is appended to exactly one level list and examined exactly once when its children are collected, so the traversal does a constant amount of work per node for O(n) overall. The nested loops are misleading: the inner for loop runs once per node in the current level, and the level sizes sum to n across the whole tree rather than multiplying. Space is O(n) — the result holds every value in the tree, and current and next_level together can hold a full level, which for the widest level of a balanced tree is roughly half the nodes.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


def level_order(root: TreeNode | None) -> list[list[int]]:
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
        current = next_level
        result.append(vals)
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

std::vector<std::vector<int>> levelOrder(TreeNode* root) {
    std::vector<std::vector<int>> result;
    if (root == nullptr) return result;
    std::vector<TreeNode*> current = {root};
    while (!current.empty()) {
        std::vector<TreeNode*> next_level;
        std::vector<int> vals;
        for (auto* node : current) {
            vals.push_back(node->val);
            if (node->left) next_level.push_back(node->left);
            if (node->right) next_level.push_back(node->right);
        }
        current = next_level;
        result.push_back(vals);
    }
    return result;
}
```

### Rust

```rust
#[derive(Debug)]
struct TreeNode {
    val: i32,
    left: Option<Box<TreeNode>>,
    right: Option<Box<TreeNode>>,
}

impl TreeNode {
    fn new(val: i32) -> Self {
        TreeNode { val, left: None, right: None }
    }
}

fn level_order(root: Option<Box<TreeNode>>) -> Vec<Vec<i32>> {
    let mut result: Vec<Vec<i32>> = Vec::new();
    let mut current: Vec<Box<TreeNode>> = Vec::new();
    if let Some(node) = root {
        current.push(node);
    }
    while !current.is_empty() {
        let mut next_level: Vec<Box<TreeNode>> = Vec::new();
        let mut vals: Vec<i32> = Vec::new();
        for mut node in current {
            vals.push(node.val);
            if let Some(left) = node.left.take() {
                next_level.push(left);
            }
            if let Some(right) = node.right.take() {
                next_level.push(right);
            }
        }
        current = next_level;
        result.push(vals);
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/binary-tree-level-order-traversal.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
