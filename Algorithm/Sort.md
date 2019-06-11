# Sort

> At least $O(n)$

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

### Complexity

#### Time 

Worst-case: smallest element is in the last position.

$O(n^2)$ for average and worst case.

#### Space

$O(1)$

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
def bubblesort(sort_list):
    swapped=True
    second_to_last_idx = len(sort_list)-2
    n = 1
    while swapped and second_to_last_idx > 0:
        swapped=False
        for i in range(second_to_last_idx+1):
            if sort_list[i] > sort_list[i+1]:
                sort_list[i], sort_list[i+1] = sort_list[i+1], sort_list[i]
                swapped = True
        second_to_last_idx -= 1
```

#### Selection Sort

Find the smallest element using a linear scan and move it to the front (swapping it with the front element). Continue doing this until all the elements are in place.

##### Complexity

**Time:** $O(n^2)$ for average and worst case.

**Space:** $O(1)$.

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

### Complexity

#### Time Complexity

$O(nlogn)$ for average and worst case.

*Merging two sorted lists can be done in linear time $O(n)$.*

#### Space complexity

Need extra space to hold the two halves (depends).

### Implementation

```python
def mergesort(sort_list, lo=0, hi=len(A)-1):
  	# if lo >= hi: return
    
    # qsort(A, lo, pivot_idx-1)
    # qsort(A, pivot_idx+1, hi)
```

## Quick Sort

### Idea

> **Like building binary search tree.**

* Pick pivot, usually choose first item, partition so elements left of pivot are less than pivot and elements right are greater (walk from head and tail, switch);
* recursively partition the left and right until small enough to sort trivially.

Can choose a pivot value from the median of head, mid, tail.

### Complexity

#### Time Complexity

Worst-case: $O(n^2)$;

Typical behavior: $O(nlogn)$

*Merging two sorted lists can be done in linear time $O(n)$.*

#### Space Complexity

$O(logn)$

### Implementation

```python
def partition(A,lo,hi):
    pivot = A[hi]    # pick last element as pivot  
    left = [a for a in A if a<pivot]
    right = [a for a in A if a>pivot]
    A[:] = left+[pivot]+right # copy back to A
    return len(left) # return index of pivot

def partition_inplace(A,lo,hi):
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

### Complexity

#### Time Complexity

> when the range of keys, $m$, the number of elements, $n$.

Best case: $m$ is similar to $n$.

$T(n,m) = n+m$, yielding $O(n)$.

#### Space Complexity

Worst-case: $O(n)$.

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

Compress number of buckets, $m$, to some fixed number instead of range of numbers.

## Bucket Sort (Bin Sort)

### Idea

Distribute n elements across m ordered buckets, sort elements within each bucket, then concatenate elements from sorted buckets in order.

**For String:** use first letter as bucket key.

### Complexity

#### Time Complexity

$T(n,m)=nlogn+m$, yielding $O(nlogn)$

- Sorting one bucket at best $O(nlogn)$;
- Walking $m$ bucket $O(m)$.

**Worst-Case:** all values are the same, putting everything into one bucket.

**Best-case:** even distribution of elements across $m$ buckets.

$T(n,m,k)=m\times k^2 \times n=\frac{n}{k} \times k^2 + n = nk + n$, yielding $O(n)$

- Choose $m$ always so $\frac{n}{m}$ is so small fixed constant size $k$;
- Sork $k$ elements $m$ times (bubble sort);
- Merge $m$ sorted lists.

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

###Idea

* Nested indexes based upon s[i];
* With nesting $k$ deep, words are sorted uniquely to first $k$ letters, giving nested bucket sort.

