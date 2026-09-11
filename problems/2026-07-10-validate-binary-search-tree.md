# Validate Binary Search Tree

**Puzzle date:** 2026-07-10  
**Category:** tree  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The dominant cost is the recursive `valid` function, which visits every node in the tree exactly once to check whether it satisfies the BST property. Each call does O(1) work (a comparison and two recursive calls), so the total time grows linearly with the number of nodes n. For space, the recursion stack is the key factor — in the worst case (a completely skewed/linear tree), you stack up n frames before hitting a base case, giving O(n) space. You might be tempted to say O(log n) space because a balanced BST has height log n, but the problem makes no guarantee about balance, so you must account for the worst-case skewed tree.

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

def is_valid_bst(root: TreeNode | None) -> bool:
    def valid(node, low, high):
        if node is None:
            return True
        if not (low < node.val < high):
            return False
        return valid(node.left, low, node.val) and valid(node.right, node.val, high)
    return valid(root, float('-inf'), float('inf'))
```

### C++

```cpp
#include <limits>

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

bool valid(TreeNode* node, long low, long high) {
    if (!node) return true;
    if (!(low < node->val && node->val < high)) return false;
    return valid(node->left, low, node->val) && valid(node->right, node->val, high);
}

bool isValidBST(TreeNode* root) {
    return valid(root, std::numeric_limits<long>::min(), std::numeric_limits<long>::max());
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

fn valid(node: &Option<Rc<RefCell<TreeNode>>>, low: i64, high: i64) -> bool {
    match node {
        None => true,
        Some(n) => {
            let n = n.borrow();
            let v = n.val as i64;
            if !(low < v && v < high) {
                return false;
            }
            valid(&n.left, low, v) && valid(&n.right, v, high)
        }
    }
}

fn is_valid_bst(root: Option<Rc<RefCell<TreeNode>>>) -> bool {
    valid(&root, i64::MIN, i64::MAX)
}
```

---

Played daily at [complexle.com](https://complexle.com).
