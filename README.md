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

**74 puzzles** archived, from 2026-06-01 to 2026-10-03.

## Recent puzzles

Showing the 30 most recent. For the full archive, browse
[`problems/`](problems/) or query [`problems.json`](problems.json).

| Date | Problem | Category | Time | Space |
|------|---------|----------|------|-------|
| 2026-10-03 | [Set Matrix Zeroes](problems/2026-10-03-set-matrix-zeroes.md) | arrays | `O(m*n)` | `O(1)` |
| 2026-10-02 | [H-Index](problems/2026-10-02-h-index.md) | arrays | `O(n)` | `O(n)` |
| 2026-10-01 | [Gas Station](problems/2026-10-01-gas-station.md) | arrays | `O(n)` | `O(1)` |
| 2026-09-30 | [Non-overlapping Intervals](problems/2026-09-30-non-overlapping-intervals.md) | arrays | `O(n log n)` | `O(log n)` |
| 2026-09-29 | [Candy](problems/2026-09-29-candy.md) | arrays | `O(n)` | `O(n)` |
| 2026-09-28 | [Summary Ranges](problems/2026-09-28-summary-ranges.md) | arrays | `O(n)` | `O(n)` |
| 2026-09-27 | [Missing Number](problems/2026-09-27-missing-number.md) | arrays | `O(n)` | `O(1)` |
| 2026-09-26 | [Single Number](problems/2026-09-26-single-number.md) | arrays | `O(n)` | `O(1)` |
| 2026-09-25 | [Find First and Last Position of Element in Sorted Array](problems/2026-09-25-find-first-and-last-position-of-element-in-sorted-array.md) | binary search | `O(log n)` | `O(1)` |
| 2026-09-24 | [Minimum Size Subarray Sum](problems/2026-09-24-minimum-size-subarray-sum.md) | sliding window | `O(n)` | `O(1)` |
| 2026-09-23 | [Longest Subarray of 1's After Deleting One Element](problems/2026-09-23-longest-subarray-of-1s-after-deleting-one-element.md) | sliding window | `O(n)` | `O(1)` |
| 2026-09-22 | [Find Peak Element](problems/2026-09-22-find-peak-element.md) | binary search | `O(log n)` | `O(1)` |
| 2026-09-21 | [Search Insert Position](problems/2026-09-21-search-insert-position.md) | binary search | `O(log n)` | `O(1)` |
| 2026-09-20 | [Subarray Product Less Than K](problems/2026-09-20-subarray-product-less-than-k.md) | sliding window | `O(n)` | `O(1)` |
| 2026-09-19 | [Minimum Window Substring](problems/2026-09-19-minimum-window-substring.md) | sliding window | `O(n + m)` | `O(m)` |
| 2026-09-18 | [Fruit Into Baskets](problems/2026-09-18-fruit-into-baskets.md) | sliding window | `O(n)` | `O(1)` |
| 2026-09-17 | [Max Consecutive Ones III](problems/2026-09-17-max-consecutive-ones-iii.md) | sliding window | `O(n)` | `O(1)` |
| 2026-09-16 | [Longest Repeating Character Replacement](problems/2026-09-16-longest-repeating-character-replacement.md) | sliding window | `O(n)` | `O(1)` |
| 2026-09-15 | [Longest Substring Without Repeating Characters](problems/2026-09-15-longest-substring-without-repeating-characters.md) | sliding window | `O(n)` | `O(min(n, m))` |
| 2026-09-14 | [Is Subsequence](problems/2026-09-14-is-subsequence.md) | two pointers | `O(n)` | `O(1)` |
| 2026-09-13 | [Valid Sudoku](problems/2026-09-13-valid-sudoku.md) | arrays | `O(1)` | `O(1)` |
| 2026-09-12 | [Backspace String Compare](problems/2026-09-12-backspace-string-compare.md) | two pointers | `O(n)` | `O(1)` |
| 2026-09-11 | [Remove Element](problems/2026-09-11-remove-element.md) | two pointers | `O(n)` | `O(1)` |
| 2026-09-10 | [Move Zeroes](problems/2026-09-10-move-zeroes.md) | two pointers | `O(n)` | `O(1)` |
| 2026-09-09 | [Reverse String](problems/2026-09-09-reverse-string.md) | two pointers | `O(n)` | `O(1)` |
| 2026-09-08 | [Partition Labels](problems/2026-09-08-partition-labels.md) | two pointers | `O(n)` | `O(n)` |
| 2026-09-07 | [Squares of a Sorted Array](problems/2026-09-07-squares-of-a-sorted-array.md) | two pointers | `O(n)` | `O(n)` |
| 2026-09-06 | [Valid Palindrome](problems/2026-09-06-valid-palindrome.md) | two pointers | `O(n)` | `O(1)` |
| 2026-09-05 | [Sort Colors](problems/2026-09-05-sort-colors.md) | two pointers | `O(n)` | `O(1)` |
| 2026-09-04 | [3Sum Closest](problems/2026-09-04-3sum-closest.md) | two pointers | `O(n^2)` | `O(1)` |

## License & attribution

Explanations and the archive tooling are © Complexle, released under the
MIT License (see [`LICENSE`](LICENSE)). Some implementations are adapted
from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions)
(MIT) — those puzzles link their upstream source, and the notice is
reproduced in [`NOTICE`](NOTICE).
