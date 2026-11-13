# Binary Tree Inorder Traversal

**Puzzle date:** 2026-11-12  
**Category:** tree  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

This is a Morris traversal. The inner while that hunts for a predecessor makes it look worse than linear, but each edge in the tree is walked at most three times across the entire run, so the total work is still O(n). The space answer is worth reading carefully: the traversal itself is genuinely O(1) auxiliary — it uses temporary right-pointer links instead of a stack or recursion, which is the whole point of the technique — but the function still allocates a result list holding all n values, and that dominates. Counting the returned list, the space is O(n).

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class TreeNode:
    def __init__(self, x: int):
        self.val = x
        self.left: Optional['TreeNode'] = None
        self.right: Optional['TreeNode'] = None


def inorder_traversal(root: Optional[TreeNode]) -> list[int]:
    result: list[int] = []
    curr = root
    while curr:
        if curr.left is None:
            result.append(curr.val)
            curr = curr.right
        else:
            node = curr.left
            while node.right and node.right != curr:
                node = node.right
            if node.right is None:
                node.right = curr
                curr = curr.left
            else:
                result.append(curr.val)
                node.right = None
                curr = curr.right
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

std::vector<int> inorderTraversal(TreeNode* root) {
    std::vector<int> res;
    TreeNode *curr = root;
    while (curr) {
        if (!curr->left) {
            res.emplace_back(curr->val);
            curr = curr->right;
        } else {
            TreeNode *node = curr->left;
            while (node->right && node->right != curr) {
                node = node->right;
            }
            if (!node->right) {
                node->right = curr;
                curr = curr->left;
            } else {
                res.emplace_back(curr->val);
                node->right = nullptr;
                curr = curr->right;
            }
        }
    }
    return res;
}
```

### Rust

```rust
type Link = Option<Rc<RefCell<TreeNode>>>;

#[derive(Debug)]
struct TreeNode {
    val: i32,
    left: Link,
    right: Link,
}

impl TreeNode {
    fn new(val: i32) -> Self {
        TreeNode { val, left: None, right: None }
    }
}

fn inorder_traversal(root: Link) -> Vec<i32> {
    let mut result = Vec::new();
    let mut curr = root;
    while let Some(curr_node) = curr.clone() {
        let left = curr_node.borrow().left.clone();
        if left.is_none() {
            result.push(curr_node.borrow().val);
            let right = curr_node.borrow().right.clone();
            curr = right;
        } else {
            let mut node = left.unwrap();
            loop {
                let right = node.borrow().right.clone();
                match right {
                    Some(r) if !Rc::ptr_eq(&r, &curr_node) => {
                        node = r;
                    }
                    _ => break,
                }
            }
            let node_right = node.borrow().right.clone();
            if node_right.is_none() {
                node.borrow_mut().right = Some(curr_node.clone());
                let left2 = curr_node.borrow().left.clone();
                curr = left2;
            } else {
                result.push(curr_node.borrow().val);
                node.borrow_mut().right = None;
                let right = curr_node.borrow().right.clone();
                curr = right;
            }
        }
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/binary-tree-inorder-traversal.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
