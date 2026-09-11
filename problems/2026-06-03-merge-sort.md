# Merge Sort

**Puzzle date:** 2026-06-03  
**Category:** sorting  
**Time complexity:** `O(n log n)`  
**Space complexity:** `O(n log n)`

## Explanation

The array is recursively divided in half O(log n) times, and at each level of recursion the merge step processes all n elements, giving O(n log n) time overall. For space, note that Python's arr[:mid] and arr[mid:] slicing creates new list copies at each recursive call; across all log n levels of recursion, the total memory allocated for these slices and the merged result arrays sums to O(n log n) rather than the O(n) you would see in an in-place merge sort implementation.

## Implementations

All three implement the same algorithm, so they share the same time and
space complexity — only the language differs.

### Python

```python
def merge_sort(arr: list[int]) -> list[int]:
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i]); i += 1
        else:
            result.append(right[j]); j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

### C++

```cpp
void merge(std::vector<int>& arr, int l, int m, int r) {
    std::vector<int> tmp(arr.begin() + l, arr.begin() + r + 1);
    int i = 0, j = m - l + 1, k = l;
    int mid = m - l;
    while (i <= mid && j < (int)tmp.size()) {
        if (tmp[i] <= tmp[j]) arr[k++] = tmp[i++];
        else arr[k++] = tmp[j++];
    }
    while (i <= mid) arr[k++] = tmp[i++];
    while (j < (int)tmp.size()) arr[k++] = tmp[j++];
}

void mergeSort(std::vector<int>& arr, int l, int r) {
    if (l >= r) return;
    int m = l + (r - l) / 2;
    mergeSort(arr, l, m);
    mergeSort(arr, m + 1, r);
    merge(arr, l, m, r);
}
```

### Rust

```rust
fn merge_sort(arr: &mut [i32]) {
    let len = arr.len();
    if len <= 1 { return; }
    let mid = len / 2;
    merge_sort(&mut arr[..mid]);
    merge_sort(&mut arr[mid..]);
    let mut tmp = arr.to_vec();
    let (mut i, mut j, mut k) = (0, mid, 0);
    while i < mid && j < len {
        if arr[i] <= arr[j] { tmp[k] = arr[i]; i += 1; }
        else { tmp[k] = arr[j]; j += 1; }
        k += 1;
    }
    tmp[k..].copy_from_slice(if i < mid { &arr[i..mid] } else { &arr[j..len] });
    arr.copy_from_slice(&tmp);
}
```

---

Played daily at [complexle.com](https://complexle.com).
