# Complexle Archive

Every retired daily puzzle from [complexle.com](https://complexle.com) —
a daily game where you guess the **time and space complexity** of a code
snippet. Each problem is implemented in Python, C++, and Rust; all three
share the same complexity, so they're directly comparable.

Updated daily, automatically, as each puzzle retires.

> **Only past puzzles appear here.** Upcoming puzzles are deliberately
> excluded so the daily game isn't spoiled.

## Contents

- [`problems.json`](problems.json) — the full dataset, one object per puzzle
- [`problems/`](problems/) — one Markdown page per puzzle, browsable on GitHub

**129 puzzles** archived, from 2026-06-01 to 2026-11-27.

## Recent puzzles

Showing the 30 most recent. For the full archive, browse
[`problems/`](problems/) or query [`problems.json`](problems.json).

| Date | Problem | Category | Time | Space |
|------|---------|----------|------|-------|
| 2026-11-27 | [Asteroid Collision](problems/2026-11-27-asteroid-collision.md) | stack | `O(n)` | `O(n)` |
| 2026-11-26 | [Contiguous Array](problems/2026-11-26-contiguous-array.md) | hash map | `O(n)` | `O(n)` |
| 2026-11-25 | [Continuous Subarray Sum](problems/2026-11-25-continuous-subarray-sum.md) | hash map | `O(n)` | `O(min(n, k))` |
| 2026-11-24 | [Construct Binary Tree from Preorder and Inorder Traversal](problems/2026-11-24-construct-binary-tree-from-preorder-and-inorder-traversal.md) | tree | `O(n)` | `O(n)` |
| 2026-11-23 | [Middle of the Linked List](problems/2026-11-23-middle-of-the-linked-list.md) | linked list | `O(n)` | `O(1)` |
| 2026-11-22 | [Word Pattern](problems/2026-11-22-word-pattern.md) | hash map | `O(n + m)` | `O(n + m)` |
| 2026-11-21 | [Search a 2D Matrix](problems/2026-11-21-search-a-2d-matrix.md) | binary search | `O(log(m * n))` | `O(1)` |
| 2026-11-20 | [Koko Eating Bananas](problems/2026-11-20-koko-eating-bananas.md) | binary search | `O(n log m)` | `O(1)` |
| 2026-11-19 | [Subarray Sum Equals K](problems/2026-11-19-subarray-sum-equals-k.md) | hash map | `O(n)` | `O(n)` |
| 2026-11-18 | [Binary Tree Level Order Traversal](problems/2026-11-18-binary-tree-level-order-traversal.md) | tree | `O(n)` | `O(n)` |
| 2026-11-17 | [Isomorphic Strings](problems/2026-11-17-isomorphic-strings.md) | hash map | `O(n)` | `O(n)` |
| 2026-11-16 | [Ransom Note](problems/2026-11-16-ransom-note.md) | hash map | `O(n + m)` | `O(1)` |
| 2026-11-15 | [Path Sum](problems/2026-11-15-path-sum.md) | tree | `O(n)` | `O(h)` |
| 2026-11-14 | [Binary Tree Right Side View](problems/2026-11-14-binary-tree-right-side-view.md) | tree | `O(n)` | `O(h)` |
| 2026-11-13 | [Add Two Numbers II](problems/2026-11-13-add-two-numbers-ii.md) | linked list | `O(n + m)` | `O(n + m)` |
| 2026-11-12 | [Binary Tree Inorder Traversal](problems/2026-11-12-binary-tree-inorder-traversal.md) | tree | `O(n)` | `O(n)` |
| 2026-11-11 | [Binary Tree Zigzag Level Order Traversal](problems/2026-11-11-binary-tree-zigzag-level-order-traversal.md) | tree | `O(n)` | `O(n)` |
| 2026-11-10 | [Odd Even Linked List](problems/2026-11-10-odd-even-linked-list.md) | linked list | `O(n)` | `O(1)` |
| 2026-11-09 | [Copy List with Random Pointer](problems/2026-11-09-copy-list-with-random-pointer.md) | linked list | `O(n)` | `O(n)` |
| 2026-11-08 | [Add Two Numbers](problems/2026-11-08-add-two-numbers.md) | linked list | `O(n + m)` | `O(n + m)` |
| 2026-11-07 | [Remove Duplicate Letters](problems/2026-11-07-remove-duplicate-letters.md) | stack | `O(n)` | `O(n)` |
| 2026-11-06 | [Next Greater Element I](problems/2026-11-06-next-greater-element-i.md) | stack | `O(n + m)` | `O(n + m)` |
| 2026-11-05 | [Maximal Rectangle](problems/2026-11-05-maximal-rectangle.md) | stack | `O(m * n)` | `O(n)` |
| 2026-11-04 | [Next Greater Element II](problems/2026-11-04-next-greater-element-ii.md) | stack | `O(n)` | `O(n)` |
| 2026-11-03 | [Largest Rectangle in Histogram](problems/2026-11-03-largest-rectangle-in-histogram.md) | stack | `O(n)` | `O(n)` |
| 2026-11-02 | [Remove All Adjacent Duplicates In String](problems/2026-11-02-remove-all-adjacent-duplicates-in-string.md) | stack | `O(n)` | `O(n)` |
| 2026-11-01 | [Last Stone Weight](problems/2026-11-01-last-stone-weight.md) | heap | `O(n log n)` | `O(n)` |
| 2026-10-31 | [Task Scheduler](problems/2026-10-31-task-scheduler.md) | heap | `O(n)` | `O(n)` |
| 2026-10-30 | [Intersection of Two Arrays](problems/2026-10-30-intersection-of-two-arrays.md) | hash map | `O(n + m)` | `O(min(n, m))` |
| 2026-10-29 | [Intersection of Two Arrays II](problems/2026-10-29-intersection-of-two-arrays-ii.md) | hash map | `O(n + m)` | `O(min(n, m))` |

## License & attribution

Explanations and the archive tooling are © Complexle, released under the
MIT License (see [`LICENSE`](LICENSE)). Some implementations are adapted
from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions)
(MIT) — those puzzles link their upstream source, and the notice is
reproduced in [`NOTICE`](NOTICE).
