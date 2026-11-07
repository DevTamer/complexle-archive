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

**108 puzzles** archived, from 2026-06-01 to 2026-11-06.

## Recent puzzles

Showing the 30 most recent. For the full archive, browse
[`problems/`](problems/) or query [`problems.json`](problems.json).

| Date | Problem | Category | Time | Space |
|------|---------|----------|------|-------|
| 2026-11-06 | [Next Greater Element I](problems/2026-11-06-next-greater-element-i.md) | stack | `O(n + m)` | `O(n + m)` |
| 2026-11-05 | [Maximal Rectangle](problems/2026-11-05-maximal-rectangle.md) | stack | `O(m*n)` | `O(n)` |
| 2026-11-04 | [Next Greater Element II](problems/2026-11-04-next-greater-element-ii.md) | stack | `O(n)` | `O(n)` |
| 2026-11-03 | [Largest Rectangle in Histogram](problems/2026-11-03-largest-rectangle-in-histogram.md) | stack | `O(n)` | `O(n)` |
| 2026-11-02 | [Remove All Adjacent Duplicates In String](problems/2026-11-02-remove-all-adjacent-duplicates-in-string.md) | stack | `O(n)` | `O(n)` |
| 2026-11-01 | [Last Stone Weight](problems/2026-11-01-last-stone-weight.md) | heap | `O(n log n)` | `O(n)` |
| 2026-10-31 | [Task Scheduler](problems/2026-10-31-task-scheduler.md) | heap | `O(n)` | `O(n)` |
| 2026-10-30 | [Intersection of Two Arrays](problems/2026-10-30-intersection-of-two-arrays.md) | hash map | `O(n + m)` | `O(min(n, m))` |
| 2026-10-29 | [Intersection of Two Arrays II](problems/2026-10-29-intersection-of-two-arrays-ii.md) | hash map | `O(n + m)` | `O(min(n, m))` |
| 2026-10-28 | [First Unique Character in a String](problems/2026-10-28-first-unique-character-in-a-string.md) | hash map | `O(n)` | `O(n)` |
| 2026-10-27 | [Longest Substring with At Most Two Distinct Characters](problems/2026-10-27-longest-substring-with-at-most-two-distinct-characters.md) | hash map | `O(n)` | `O(1)` |
| 2026-10-26 | [4Sum II](problems/2026-10-26-4sum-ii.md) | hash map | `O(n²)` | `O(n²)` |
| 2026-10-25 | [Find Minimum in Rotated Sorted Array](problems/2026-10-25-find-minimum-in-rotated-sorted-array.md) | binary search | `O(log n)` | `O(1)` |
| 2026-10-24 | [Valid Anagram](problems/2026-10-24-valid-anagram.md) | hash map | `O(n)` | `O(1)` |
| 2026-10-23 | [Merge Intervals](problems/2026-10-23-merge-intervals.md) | sorting | `O(n log n)` | `O(n)` |
| 2026-10-22 | [Top K Frequent Elements](problems/2026-10-22-top-k-frequent-elements.md) | heap | `O(n log k)` | `O(n)` |
| 2026-10-21 | [Maximum Product Subarray](problems/2026-10-21-maximum-product-subarray.md) | dynamic programming | `O(n)` | `O(1)` |
| 2026-10-20 | [Longest Palindromic Substring](problems/2026-10-20-longest-palindromic-substring.md) | two pointers | `O(n²)` | `O(1)` |
| 2026-10-19 | [Longest Increasing Subsequence](problems/2026-10-19-longest-increasing-subsequence.md) | dynamic programming | `O(n log n)` | `O(n)` |
| 2026-10-18 | [Daily Temperatures](problems/2026-10-18-daily-temperatures.md) | stack | `O(n)` | `O(n)` |
| 2026-10-17 | [Spiral Matrix](problems/2026-10-17-spiral-matrix.md) | arrays | `O(m*n)` | `O(m*n)` |
| 2026-10-16 | [Jump Game](problems/2026-10-16-jump-game.md) | arrays | `O(n)` | `O(1)` |
| 2026-10-15 | [Validate Binary Search Tree](problems/2026-10-15-validate-binary-search-tree.md) | tree | `O(n)` | `O(n)` |
| 2026-10-14 | [Diameter of Binary Tree](problems/2026-10-14-diameter-of-binary-tree.md) | tree | `O(n)` | `O(n)` |
| 2026-10-13 | [Invert Binary Tree](problems/2026-10-13-invert-binary-tree.md) | tree | `O(n)` | `O(h)` |
| 2026-10-12 | [Symmetric Tree](problems/2026-10-12-symmetric-tree.md) | tree | `O(n)` | `O(n)` |
| 2026-10-11 | [Pascal's Triangle](problems/2026-10-11-pascals-triangle.md) | arrays | `O(n²)` | `O(n²)` |
| 2026-10-10 | [Remove Duplicates from Sorted Array](problems/2026-10-10-remove-duplicates-from-sorted-array.md) | two pointers | `O(n)` | `O(1)` |
| 2026-10-09 | [Linked List Cycle](problems/2026-10-09-linked-list-cycle.md) | cycle detection | `O(n)` | `O(1)` |
| 2026-10-08 | [Merge Two Sorted Lists](problems/2026-10-08-merge-two-sorted-lists.md) | linked list | `O(n + m)` | `O(1)` |

## License & attribution

Explanations and the archive tooling are © Complexle, released under the
MIT License (see [`LICENSE`](LICENSE)). Some implementations are adapted
from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions)
(MIT) — those puzzles link their upstream source, and the notice is
reproduced in [`NOTICE`](NOTICE).
