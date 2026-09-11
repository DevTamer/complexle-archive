# Symmetric Tree

**Puzzle date:** 2026-07-07  
**Category:** tree  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the recursive `mirror` function, which visits each node in the tree exactly once (pairing nodes symmetrically from left and right subtrees). Every node is compared at most one time, so the total work scales linearly with the number of nodes n. The space complexity is also O(n) because the call stack can grow as deep as the height of the tree — in the worst case (a completely skewed tree), that height is n. You might be tempted to say O(log n) space, which would only be true for a perfectly balanced tree where height is log n, but the algorithm must handle unbalanced trees too.

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

def is_symmetric(root: TreeNode | None) -> bool:
    def mirror(a, b):
        if a is None and b is None:
            return True
        if a is None or b is None or a.val != b.val:
            return False
        return mirror(a.left, b.right) and mirror(a.right, b.left)
    return root is None or mirror(root.left, root.right)
```

### C++

```cpp
struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

bool mirror(TreeNode* a, TreeNode* b) {
    if (!a && !b) return true;
    if (!a || !b || a->val != b->val) return false;
    return mirror(a->left, b->right) && mirror(a->right, b->left);
}

bool isSymmetric(TreeNode* root) {
    return !root || mirror(root->left, root->right);
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

fn mirror(a: Option<Rc<RefCell<TreeNode>>>, b: Option<Rc<RefCell<TreeNode>>>) -> bool {
    match (a, b) {
        (None, None) => true,
        (Some(a), Some(b)) => {
            let (a, b) = (a.borrow(), b.borrow());
            a.val == b.val
                && mirror(a.left.clone(), b.right.clone())
                && mirror(a.right.clone(), b.left.clone())
        }
        _ => false,
    }
}

fn is_symmetric(root: Option<Rc<RefCell<TreeNode>>>) -> bool {
    match root {
        None => true,
        Some(node) => {
            let n = node.borrow();
            mirror(n.left.clone(), n.right.clone())
        }
    }
}
```

---

Played daily at [complexle.com](https://complexle.com).
