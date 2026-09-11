# Lowest Common Ancestor of a BST

**Puzzle date:** 2026-06-24  
**Category:** tree  
**Time complexity:** `O(h)`  
**Space complexity:** `O(h)`

## Explanation

The dominant cost is the recursive traversal down a single path from the root to the lowest common ancestor node. At each step, the BST property lets you decide to go left, right, or stop — so you never visit more than one branch, and you descend at most h levels where h is the height of the tree. The space complexity is also O(h) because each recursive call adds a frame to the call stack, and you make at most h recursive calls before returning. You might be tempted to say O(log n) for a balanced BST, but that's only a special case — in the worst case (a skewed tree), h equals n, so O(h) is the correct general answer. Similarly, O(1) space is wrong because this recursive implementation uses the call stack proportional to the depth traversed.

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

def lowest_common_ancestor(root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
    if p.val < root.val and q.val < root.val:
        return lowest_common_ancestor(root.left, p, q)
    if p.val > root.val and q.val > root.val:
        return lowest_common_ancestor(root.right, p, q)
    return root
```

### C++

```cpp
struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (p->val < root->val && q->val < root->val)
        return lowestCommonAncestor(root->left, p, q);
    if (p->val > root->val && q->val > root->val)
        return lowestCommonAncestor(root->right, p, q);
    return root;
}
```

### Rust

```rust
type Link = Option<Rc<RefCell<TreeNode>>>;

struct TreeNode { val: i32, left: Link, right: Link }

fn lowest_common_ancestor(root: Link, p: i32, q: i32) -> Link {
    let node = root.clone()?;
    let v = node.borrow().val;
    if p < v && q < v {
        return lowest_common_ancestor(node.borrow().left.clone(), p, q);
    }
    if p > v && q > v {
        return lowest_common_ancestor(node.borrow().right.clone(), p, q);
    }
    root
}
```

---

Played daily at [complexle.com](https://complexle.com).
