# Binary Tree Right Side View

**Puzzle date:** 2026-11-14  
**Category:** tree  
**Time complexity:** `O(n)`  
**Space complexity:** `O(h)`

## Explanation

The depth-first search visits every node exactly once — the right subtree first, so the first node reached at each new depth is the rightmost one — doing constant work per node, which gives O(n). Only one value per level is kept, but that does not reduce the traversal cost, since every node must still be examined. Space is O(h), driven by the recursion stack, which holds one frame per level on the current root-to-leaf path. For a balanced tree that is about log n, but for a degenerate single-branch tree it grows to n, so h rather than log n is the honest bound.

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


def right_side_view(root: TreeNode | None) -> list[int]:
    result: list[int] = []

    def dfs(node: TreeNode | None, depth: int) -> None:
        if not node:
            return
        if depth > len(result):
            result.append(node.val)
        dfs(node.right, depth + 1)
        dfs(node.left, depth + 1)

    dfs(root, 1)
    return result
```

### C++

```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

void rightSideViewDFS(TreeNode* node, int depth, std::vector<int>& result) {
    if (!node) return;
    if (depth > (int)result.size()) {
        result.push_back(node->val);
    }
    rightSideViewDFS(node->right, depth + 1, result);
    rightSideViewDFS(node->left, depth + 1, result);
}

std::vector<int> rightSideView(TreeNode* root) {
    std::vector<int> result;
    rightSideViewDFS(root, 1, result);
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

fn right_side_view(root: Option<Box<TreeNode>>) -> Vec<i32> {
    let mut result = Vec::new();

    fn dfs(node: &Option<Box<TreeNode>>, depth: usize, result: &mut Vec<i32>) {
        if let Some(n) = node {
            if depth > result.len() {
                result.push(n.val);
            }
            dfs(&n.right, depth + 1, result);
            dfs(&n.left, depth + 1, result);
        }
    }

    dfs(&root, 1, &mut result);
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/binary-tree-right-side-view.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
