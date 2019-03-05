# 1.3. Sort

at least $O(n)$

## Bubble Sort

###Algorithm

Keep swapping until nothing changes.

![image-20190222101500986](/Users/crystal/dataScientistNotes/Algorithm/image/bubble_sort.png)

### Time Complexity

Worst-case: smallest element is in the last position.

$T(n) = n$

$O(n^2)$

## Merge Sort

### Idea

Split currently active region in half, sorting both the left and right subregions, then merge two sorted subregions

### Time Complexity

$O(nlogn)$

*Merging two sorted lists can be done in linear time.*

## Quick Sort

### Idea

Pick pivot, partition so elements left of pivot are less than pivot and elements right are greater (not sorting here); recursively partition the left and right until small enough to sort trivially.

**Like building binary search tree.**



### Time Complexity

Worst-case: $O(n^2)$; Typical behavior: $O(nlogn)$

*Merging two sorted lists can be done in linear time.*

## Pigeonhole Sort

### Idea

Map each key to unique pigeonhole in ordered range of holes; then just walk pigeonholes in order to get sorted elements.

### Time Complexity

Worst-case: when the range of keys, $m$, the number of elements, $n$.

$T(n,m) = n+m$

### Problem

When $m >> n$: sort 2 numbers, $5, 500000$, $T(n,m) = 5+5000000$.

Compress number of buckets, $m$, to some fixed number instead of range of numbers.

## Bucket Sort (Bin Sort)

### Idea

Distribute n elements across m ordered buckets, sort elements within each bucket, then concatenate elements from sorted buckets in order.

### Time Complexity

Worst-Case: all values are the same, putting everything into one bucket.

$T(n,m)=nlogn+m$

$O(nlogn)​$

Best-case: even distribution of elements across $m$ buckets.

* Choose $m$ always so $\frac{n}{m}$ is so small fixed constant size $k$.
* Sork $k$ elements $m$ times (bubble sort), merge $m$ sorted lists

$T(n,m,k)=m\times k^2 \times n$

$T(n,k)=\frac{n}{k} \times k^2 + n = nk + n$

$O(n)​$

