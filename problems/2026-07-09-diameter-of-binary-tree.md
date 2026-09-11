# Diameter of Binary Tree

**Puzzle date:** 2026-07-09  
**Category:** tree  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the recursive `height` function, which visits every node in the tree exactly once. Each node triggers a constant amount of work (two recursive calls, a max operation, and an addition), so the total time grows linearly with the number of nodes n. You might be tempted to say O(log n) because binary trees are involved, but that only applies to balanced trees — in the worst case (a completely skewed tree), the recursion goes n levels deep, not log n. The space complexity is also O(n) because the call stack can grow as deep as the height of the tree, which in the worst case (a linear chain of nodes) equals n frames.

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

def diameter_of_binary_tree(root: TreeNode | None) -> int:
    diameter = 0
    def height(node):
        nonlocal diameter
        if node is None:
            return 0
        left = height(node.left)
        right = height(node.right)
        diameter = max(diameter, left + right)
        return 1 + max(left, right)
    height(root)
    return diameter
```

### C++

```cpp
#include <algorithm>

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

int height(TreeNode* node, int& diameter) {
    if (!node) return 0;
    int left = height(node->left, diameter);
    int right = height(node->right, diameter);
    diameter = std::max(diameter, left + right);
    return 1 + std::max(left, right);
}

int diameterOfBinaryTree(TreeNode* root) {
    int diameter = 0;
    height(root, diameter);
    return diameter;
}
```

### Rust

```rust
use std::cell::RefCell;
use std::rc::Rc;

struct TreeNode {
    val: i32,
    left: Option<Rc<RefCell<TreeNode>>>,
    right: Option<Rc<RefCell<TreeNode>>>,
}

fn height(node: &Option<Rc<RefCell<TreeNode>>>, diameter: &mut i32) -> i32 {
    match node {
        None => 0,
        Some(n) => {
            let n = n.borrow();
            let left = height(&n.left, diameter);
            let right = height(&n.right, diameter);
            *diameter = (*diameter).max(left + right);
            1 + left.max(right)
        }
    }
}

fn diameter_of_binary_tree(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
    let mut diameter = 0;
    height(&root, &mut diameter);
    diameter
}
```

---

Played daily at [complexle.com](https://complexle.com).
