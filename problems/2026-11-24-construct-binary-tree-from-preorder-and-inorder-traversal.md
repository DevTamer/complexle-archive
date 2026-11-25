# Construct Binary Tree from Preorder and Inorder Traversal

**Puzzle date:** 2026-11-24  
**Category:** tree  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

The lookup map is built in one pass, and it is what keeps the construction linear: without it, finding the root's position in the inorder array would require a scan at every level, which is the O(n²) trap. With constant-time index lookups, build creates each node exactly once for O(n). The level-order serialisation that follows is another linear pass, walking the queue with an index cursor rather than repeatedly removing from the front. Space is O(n): the lookup map holds an entry per value, the constructed tree holds n nodes, and the output list holds one slot per node plus its empty children.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
class TreeNode:
    def __init__(self, val: int):
        self.val = val
        self.left: Optional["TreeNode"] = None
        self.right: Optional["TreeNode"] = None

def build_tree(preorder: list[int], inorder: list[int]) -> list[int | None]:
    lookup = {num: i for i, num in enumerate(inorder)}

    def build(pre_start: int, in_start: int, in_end: int) -> Optional[TreeNode]:
        if in_start == in_end:
            return None
        node = TreeNode(preorder[pre_start])
        i = lookup[preorder[pre_start]]
        node.left = build(pre_start + 1, in_start, i)
        node.right = build(pre_start + 1 + i - in_start, i + 1, in_end)
        return node

    root = build(0, 0, len(inorder))

    result: list[int | None] = []
    queue: list[Optional[TreeNode]] = [root]
    head = 0
    while head < len(queue):
        node = queue[head]
        head += 1
        if node is None:
            result.append(None)
        else:
            result.append(node.val)
            queue.append(node.left)
            queue.append(node.right)

    while result and result[-1] is None:
        result.pop()

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

TreeNode* buildTreeRecu(std::unordered_map<int, int>& lookup, std::vector<int>& preorder, std::vector<int>& inorder,
                         int pre_start, int in_start, int in_end) {
    if (in_start == in_end) return nullptr;
    TreeNode* node = new TreeNode(preorder[pre_start]);
    int i = lookup[preorder[pre_start]];
    node->left = buildTreeRecu(lookup, preorder, inorder, pre_start + 1, in_start, i);
    node->right = buildTreeRecu(lookup, preorder, inorder, pre_start + 1 + i - in_start, i + 1, in_end);
    return node;
}

std::vector<std::optional<int>> buildTree(std::vector<int>& preorder, std::vector<int>& inorder) {
    std::unordered_map<int, int> lookup;
    for (int i = 0; i < (int)inorder.size(); i++) {
        lookup[inorder[i]] = i;
    }
    TreeNode* root = buildTreeRecu(lookup, preorder, inorder, 0, 0, (int)inorder.size());

    std::vector<std::optional<int>> result;
    std::queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        if (node == nullptr) {
            result.push_back(std::nullopt);
        } else {
            result.push_back(node->val);
            q.push(node->left);
            q.push(node->right);
        }
    }
    while (!result.empty() && !result.back().has_value()) {
        result.pop_back();
    }
    return result;
}
```

### Rust

```rust
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

fn build_tree_recu(
    lookup: &HashMap<i32, usize>,
    preorder: &[i32],
    pre_start: usize,
    in_start: usize,
    in_end: usize,
) -> Option<Box<TreeNode>> {
    if in_start == in_end {
        return None;
    }
    let mut node = TreeNode::new(preorder[pre_start]);
    let i = lookup[&preorder[pre_start]];
    node.left = build_tree_recu(lookup, preorder, pre_start + 1, in_start, i);
    node.right = build_tree_recu(lookup, preorder, pre_start + 1 + i - in_start, i + 1, in_end);
    Some(Box::new(node))
}

fn build_tree(preorder: &[i32], inorder: &[i32]) -> Vec<Option<i32>> {
    let mut lookup = HashMap::new();
    for (i, &num) in inorder.iter().enumerate() {
        lookup.insert(num, i);
    }
    let root = build_tree_recu(&lookup, preorder, 0, 0, inorder.len());

    let mut result: Vec<Option<i32>> = Vec::new();
    let mut queue: VecDeque<Option<Box<TreeNode>>> = VecDeque::new();
    queue.push_back(root);
    while let Some(node_opt) = queue.pop_front() {
        match node_opt {
            None => result.push(None),
            Some(node) => {
                result.push(Some(node.val));
                queue.push_back(node.left);
                queue.push_back(node.right);
            }
        }
    }
    while let Some(&None) = result.last() {
        result.pop();
    }
    result
}
```

## Attribution

Adapted from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions/blob/master/Python/construct-binary-tree-from-preorder-and-inorder-traversal.py) (MIT License).

---

Played daily at [complexle.com](https://complexle.com).
