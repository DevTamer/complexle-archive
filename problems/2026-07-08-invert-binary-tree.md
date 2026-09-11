# Invert Binary Tree

**Puzzle date:** 2026-07-08  
**Category:** tree  
**Time complexity:** `O(n)`  
**Space complexity:** `O(h)`

## Explanation

The dominant cost is the recursive traversal of every node in the tree. Each call to invert_tree visits exactly one node and makes two recursive calls, so the function is called once per node — giving you O(n) time where n is the total number of nodes. The space complexity is driven by the call stack depth, which equals the height h of the tree; in the worst case (a completely skewed tree), h = n, but for a balanced tree h = log n, so we write O(h) to be precise. You might be tempted to say O(log n) for space, but that only holds for a perfectly balanced tree — a skewed tree pushes the call stack to O(n) depth, so O(h) is the correct general answer. Similarly, O(1) space is wrong because the recursive calls do consume stack frames proportional to the tree's height.

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

def invert_tree(root: TreeNode | None) -> TreeNode | None:
    if root is None:
        return None
    root.left, root.right = invert_tree(root.right), invert_tree(root.left)
    return root
```

### C++

```cpp
struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* invertTree(TreeNode* root) {
    if (!root) return nullptr;
    TreeNode* left = invertTree(root->left);
    TreeNode* right = invertTree(root->right);
    root->left = right;
    root->right = left;
    return root;
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

fn invert_tree(root: Option<Rc<RefCell<TreeNode>>>) -> Option<Rc<RefCell<TreeNode>>> {
    if let Some(node) = &root {
        let (left, right) = {
            let n = node.borrow();
            (n.left.clone(), n.right.clone())
        };
        node.borrow_mut().left = invert_tree(right);
        node.borrow_mut().right = invert_tree(left);
    }
    root
}
```

---

Played daily at [complexle.com](https://complexle.com).
