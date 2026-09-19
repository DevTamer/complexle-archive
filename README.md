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

**59 puzzles** archived, from 2026-06-01 to 2026-09-18.

## Recent puzzles

Showing the 30 most recent. For the full archive, browse
[`problems/`](problems/) or query [`problems.json`](problems.json).

| Date | Problem | Category | Time | Space |
|------|---------|----------|------|-------|
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
| 2026-09-03 | [Rotate Array](problems/2026-09-03-rotate-array.md) | arrays | `O(n)` | `O(1)` |
| 2026-09-02 | [Wiggle Subsequence](problems/2026-09-02-wiggle-subsequence.md) | arrays | `O(n)` | `O(1)` |
| 2026-09-01 | [Two Sum II - Input Array Is Sorted](problems/2026-09-01-two-sum-ii---input-array-is-sorted.md) | two pointers | `O(n)` | `O(1)` |
| 2026-08-31 | [Majority Element II](problems/2026-08-31-majority-element-ii.md) | arrays | `O(n)` | `O(1)` |
| 2026-08-30 | [Plus One](problems/2026-08-30-plus-one.md) | arrays | `O(n)` | `O(1)` |
| 2026-08-29 | [Meeting Rooms II](problems/2026-08-29-meeting-rooms-ii.md) | arrays | `O(n log n)` | `O(n)` |
| 2026-08-28 | [Pascal's Triangle II](problems/2026-08-28-pascals-triangle-ii.md) | arrays | `O(n²)` | `O(n)` |
| 2026-08-27 | [Can Place Flowers](problems/2026-08-27-can-place-flowers.md) | arrays | `O(n)` | `O(n)` |
| 2026-08-26 | [4Sum](problems/2026-08-26-4sum.md) | arrays | `O(n^3)` | `O(n)` |
| 2026-08-25 | [3Sum](problems/2026-08-25-3sum.md) | arrays | `O(n^2)` | `O(n)` |
| 2026-08-24 | [Max Consecutive Ones](problems/2026-08-24-max-consecutive-ones.md) | arrays | `O(n)` | `O(1)` |
| 2026-08-23 | [Single Number II](problems/2026-08-23-single-number-ii.md) | arrays | `O(n)` | `O(1)` |
| 2026-08-22 | [Insert Interval](problems/2026-08-22-insert-interval.md) | arrays | `O(n)` | `O(n)` |
| 2026-08-21 | [Rotate Image](problems/2026-08-21-rotate-image.md) | arrays | `O(n^2)` | `O(1)` |
| 2026-08-20 | [First Missing Positive](problems/2026-08-20-first-missing-positive.md) | arrays | `O(n)` | `O(1)` |

## License & attribution

Explanations and the archive tooling are © Complexle, released under the
MIT License (see [`LICENSE`](LICENSE)). Some implementations are adapted
from [kamyu104/LeetCode-Solutions](https://github.com/kamyu104/LeetCode-Solutions)
(MIT) — those puzzles link their upstream source, and the notice is
reproduced in [`NOTICE`](NOTICE).
