# Sort

At least $O(n)$

## DSU

- Decorate: a sequence by building a list of tuples with one or more sort keys preceding the elements from the sequence;
- Sort: the list of tuples using the Python built-in `sort`;
- Undecorate: by extracting the sorted elements of the sequence.

#### Swap

Using simultaneous assignment in `Python` to exchange items without temporary storage:

```python
a, b = b, a
```

With temporary storage:

```c
temp = alist[i]
alist[i] = alist[j]
alist[j] = temp
```

## Bubble Sort

###Idea

Keep swapping until nothing changes.

![bubble_sort](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/Algorithm/image/bubble_sort.png)

### Time Complexity

Worst-case: smallest element is in the last position.

$O(n^2)​$

### Implementation

```python
def bubblesort(sort_list):
  	for n in range(len(sort_list)-1,1,-1):
      	for i in range(n):
          	if sort_list[i]>sort_list[i+1]:
              	sort_list[i], sort_list[i+1] = sort_list[i+1], sort_list[i]
```

### Improvement

#### Short Bubble

Stop early if no exchange happened in a whole inner loop. $O(n^2)$

```python
def bubble(A):
    swapped=True
    second_to_last_idx = len(A)-2
    n = 1
    while swapped and second_to_last_idx > 0:
        swapped=False
        for i in range(second_to_last_idx+1):
            if A[i] > A[i+1]:
                A[i], A[i+1] = A[i+1], A[i]
                swapped = True
        second_to_last_idx -= 1
```

#### Selection Sort

Exchange only once for outer loop. $O(n^2)$

## Insertion Sort

### Idea

It always maintains a sorted sublist in the lower positions of the list. Each new item is then “inserted” back into the previous sublist such that the sorted sublist is one item larger.

### Time Complexity

$O(n^2)$

### Improvement

#### Shell Sort

* Breaking the original list into a number of smaller sublists (instead of breaking the list into sublists of contiguous items, the shell sort uses an increment `i`, sometimes called the **gap**, to create a sublist by choosing all items that are `i` items apart);
* Each of which is sorted using an insertion sort;
* Run insertion sort on all.
* Between $O(n)$ and $O(n^2)$

## Merge Sort

### Idea

* Split currently active region in half;
* Sorting both the left and right subregions;
* Merge two sorted subregions.

### Time Complexity

$O(nlogn)$

*Merging two sorted lists can be done in linear time.*

**Space complexity:** Need extra space to hold the two halves.

## Quick Sort

### Idea

* Pick pivot, usually choose first item, partition so elements left of pivot are less than pivot and elements right are greater (walk from head and tail, switch);
* recursively partition the left and right until small enough to sort trivially.

**Like building binary search tree.**

Can choose a pivot value from the median of head, mid, tail.

### Time Complexity

Worst-case: $O(n^2)​$; Typical behavior: $O(nlogn)​$

*Merging two sorted lists can be done in linear time.*

### Implementation

```python
def partition(A,lo,hi):
    pivot = A[hi]    # pick last element as pivot  
    left = [a for a in A if a<pivot]
    right = [a for a in A if a>pivot]
    A[:] = left+[pivot]+right # copy back to A
    return len(left) # return index of pivot

def partition_inplace(A,lo,hi):
    """
    Wikipedia: reorder the array so that all elements with
    values less than the pivot come before the pivot, while
    all elements with values greater than the pivot come after
    it (equal values can go either way).
    """
    i = lo
    pivot = A[hi]    # pick last element as pivot  
    for j in range(lo, hi):  
        if A[j] < pivot:   
            A[i], A[j] = A[j], A[i]
            i += 1  
    A[i], A[hi] = A[hi], A[i]
    return i


def qsort(A, lo=0, hi=len(A)-1):
    if lo >= hi: return
    pivot_idx = partition(A,lo,hi)
    qsort(A, lo, pivot_idx-1)
    qsort(A, pivot_idx+1, hi)
```

## Pigeonhole Sort

### Idea

Map each key to unique pigeonhole in ordered range of holes; then just walk pigeonholes in order to get sorted elements.

### Time Complexity

Worst-case: when the range of keys, $m$, the number of elements, $n$.

$T(n,m) = n+m$, yielding $O(n)$

### Implementation

```python
# avoid negative numbers for simplicity
# also assume min(A) is close to 0
def psort(A:list) -> list:
    size = max(A) + 1
    holes = [0] * size
    for a in A:
        holes[a] += 1
    A_ = []
    for i in range(0,size):
        for j in range(holes[i]):
            A_.append(i)
    return A_
```

### Problem

When $m >> n$: sort 2 numbers, $5, 500000$, $T(n,m) = 5+5000000$.

Compress number of buckets, $m​$, to some fixed number instead of range of numbers.

## Bucket Sort (Bin Sort)

### Idea

Distribute n elements across m ordered buckets, sort elements within each bucket, then concatenate elements from sorted buckets in order.

### Time Complexity

Worst-Case: all values are the same, putting everything into one bucket.

$T(n,m)=nlogn+m​$, yielding $O(nlogn)​$

Best-case: even distribution of elements across $m$ buckets.

* Choose $m$ always so $\frac{n}{m}$ is so small fixed constant size $k$.
* Sork $k$ elements $m$ times (bubble sort), merge $m$ sorted lists

$T(n,m,k)=m\times k^2 \times n=\frac{n}{k} \times k^2 + n = nk + n$, yielding $O(n)$

### Implementation

```python
import numpy as np

def bsort(A:list, nbuckets) -> list:
    mx = max(A)
    buckets = []
    max_bucket_idx = nbuckets+1
    for i in range(max_bucket_idx + 1):
        buckets.append([])
    for a in A:
        a_normalized = a / mx # get in 0..1
        i = int(a_normalized * nbuckets) # spread across buckets
        buckets[i].append(a)
        
    A_ = []
    for i in range(max_bucket_idx+1):
        A_.extend( sorted(buckets[i]) )
    return A_
```

## Nested Bucket Sort (on string)

* Nested indexes based upon s[i];
* With nesting $k$ deep, words are sorted uniquely to first $k$ letters, giving nested bucket sort.

