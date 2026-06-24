# Complexity Analysis: Bubble Sort, Merge Sort, and Quicksort

## Bubble Sort — Complexity Analysis

**Time Complexity:**

| Case | Complexity | Explanation |
|------|-----------|-------------|
| Best Case | O(n) | With the early-exit optimization (stop if no swaps occur in a pass), a sorted array requires only one full pass — n−1 comparisons and zero swaps. |
| Average Case | O(n²) | On a randomly ordered array, each of the n passes performs roughly n/2 comparisons and swaps on average, yielding approximately n²/2 operations. |
| Worst Case | O(n²) | A reverse-sorted array forces every possible comparison and swap: (n−1) + (n−2) + … + 1 = n(n−1)/2 ≈ n²/2 operations. |

**Space Complexity:** O(1) — Bubble sort is an in-place algorithm; it requires only a single temporary variable for swapping and a boolean flag for the early-exit optimization. Memory usage does not grow with input size.

**Stability:** Stable — equal elements are never swapped past each other, so their original relative order is preserved.

**Key insight:** The quadratic time complexity arises because each pass bubbles only one element into its correct position, and each pass still scans the full unsorted portion. Bubble sort's constant factors are also poor — it performs far more swaps than insertion sort for the same O(n²) bound, making it slower in practice despite equivalent asymptotic complexity.

---

## Merge Sort — Complexity Analysis

**Time Complexity:**

| Case | Complexity | Explanation |
|------|-----------|-------------|
| Best Case | O(n log n) | Regardless of input order, merge sort always divides the array in half recursively and merges — the structure of the algorithm is the same for all inputs. |
| Average Case | O(n log n) | The recurrence T(n) = 2T(n/2) + O(n) (two recursive halves plus a linear merge step) solves by the Master Theorem to Θ(n log n). |
| Worst Case | O(n log n) | Same as average — the divide-and-merge structure guarantees n log n comparisons regardless of the initial order of elements. |

**Space Complexity:** O(n) — Merge sort requires auxiliary arrays during the merge step. At any point in the recursion, the total extra memory across all active merge operations is proportional to n. The recursion stack itself adds O(log n) depth, which is dominated by the O(n) merge buffers.

**Stability:** Stable — the merge procedure preserves the original order of equal elements by favoring the left subarray when elements compare as equal.

**Key insight:** Merge sort's guaranteed O(n log n) worst-case performance makes it the algorithm of choice when predictability matters. The logarithmic factor comes from the recursion depth (log₂ n levels of splitting), while the n factor comes from the linear work performed at each level. The primary cost is the O(n) auxiliary space, which disqualifies it for memory-constrained in-place requirements.

---

## Quicksort — Complexity Analysis

**Time Complexity:**

| Case | Complexity | Explanation |
|------|-----------|-------------|
| Best Case | O(n log n) | Achieved when each partition splits the array into two equal halves, producing a balanced recursion tree of depth log n, each level doing O(n) partition work. |
| Average Case | O(n log n) | Over all possible input orderings with a random or median-of-three pivot, the expected number of comparisons is approximately 2n ln n ≈ 1.39 n log₂ n — slightly worse than merge sort's constant factor but still Θ(n log n). |
| Worst Case | O(n²) | Occurs when the pivot is always the smallest or largest element (e.g., sorted input with a naïve first-element pivot), producing partitions of size 0 and n−1 at every level — a recursion tree of depth n rather than log n. |

**Space Complexity:** O(log n) average, O(n) worst case — Quicksort is in-place (no auxiliary arrays needed for partitioning), but the recursion stack depth determines its space use. A balanced partition tree reaches depth log n; a degenerate partition tree reaches depth n. Tail-call optimization on the smaller partition bounds worst-case stack depth to O(log n).

**Stability:** Not stable — the partition step may reorder equal elements relative to each other, so their original order is not guaranteed.

**Key insight:** Despite sharing the same average-case complexity as merge sort, quicksort is typically faster in practice due to better cache performance (sequential memory access during in-place partitioning) and lower constant factors. The O(n²) worst case is avoided in practice through randomized pivot selection or median-of-three pivot strategy, which reduces the probability of degenerate partitions to negligibly small levels.

---

## Side-by-Side Complexity Summary

| Algorithm | Best Time | Average Time | Worst Time | Space | Stable |
|-----------|-----------|-------------|------------|-------|--------|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quicksort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
