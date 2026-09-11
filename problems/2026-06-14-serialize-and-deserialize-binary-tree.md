# Serialize and Deserialize Binary Tree

**Puzzle date:** 2026-06-14  
**Category:** tree  
**Time complexity:** `O(n)`  
**Space complexity:** `O(n)`

## Explanation

Both serialize and deserialize perform a BFS traversal visiting each of the n nodes exactly once, so time complexity is O(n). The space complexity is also O(n) because the queue can hold at most O(n) nodes at a time (in a complete binary tree the last level has n/2 nodes), and the result array/string stores a representation proportional to n nodes.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
from collections import deque

class Codec:
    def serialize(self, root) -> str:
        if not root:
            return "null"
        result = []
        queue = deque([root])
        while queue:
            node = queue.popleft()
            if node:
                result.append(str(node.val))
                queue.append(node.left)
                queue.append(node.right)
            else:
                result.append("null")
        return ",".join(result)

    def deserialize(self, data: str):
        if data == "null":
            return None
        vals = data.split(",")
        root = TreeNode(int(vals[0]))
        queue = deque([root])
        i = 1
        while queue:
            node = queue.popleft()
            if vals[i] != "null":
                node.left = TreeNode(int(vals[i]))
                queue.append(node.left)
            i += 1
            if vals[i] != "null":
                node.right = TreeNode(int(vals[i]))
                queue.append(node.right)
            i += 1
        return root
```

### C++

```cpp
#include <string>
#include <queue>
#include <sstream>

struct TreeNode { int val; TreeNode *left, *right; };

std::string serialize(TreeNode* root) {
    if (!root) return "null";
    std::string result;
    std::queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        auto node = q.front(); q.pop();
        if (node) {
            result += std::to_string(node->val) + ",";
            q.push(node->left);
            q.push(node->right);
        } else {
            result += "null,";
        }
    }
    return result;
}

TreeNode* deserialize(std::string data) {
    if (data == "null") return nullptr;
    std::istringstream ss(data);
    std::string token;
    std::getline(ss, token, ',');
    auto root = new TreeNode{std::stoi(token), nullptr, nullptr};
    std::queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        auto node = q.front(); q.pop();
        if (std::getline(ss, token, ',') && token != "null") {
            node->left = new TreeNode{std::stoi(token), nullptr, nullptr};
            q.push(node->left);
        }
        if (std::getline(ss, token, ',') && token != "null") {
            node->right = new TreeNode{std::stoi(token), nullptr, nullptr};
            q.push(node->right);
        }
    }
    return root;
}
```

### Rust

```rust
use std::collections::VecDeque;

fn serialize(root: Option<Box<TreeNode>>) -> String {
    let Some(root) = root else { return "null".into() };
    let mut result = Vec::new();
    let mut queue = VecDeque::new();
    queue.push_back(Some(root));
    while let Some(node_opt) = queue.pop_front() {
        match node_opt {
            Some(node) => {
                result.push(node.val.to_string());
                queue.push_back(node.left.map(|n| *n).map(Box::new));
                queue.push_back(node.right.map(|n| *n).map(Box::new));
            }
            None => result.push("null".into()),
        }
    }
    result.join(",")
}
```

---

Played daily at [complexle.com](https://complexle.com).
