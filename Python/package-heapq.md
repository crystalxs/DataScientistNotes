# heapq

> This module provides an implementation of the heap queue algorithm, also known as the priority queue algorithm.

The interesting property of a heap is that its **smallest** element is always the root, `heap[0]`.

* Zero-based indexing. This makes the relationship between the index for a node and the indexes for its children slightly less obvious, but is more suitable since Python uses zero-based indexing.
* Our pop method returns the smallest item, not the largest (called a “min heap” in textbooks; a “max heap” is more common in texts because of its suitability for in-place sorting).

## Declaration

```python
# initialized
heap = []
# transform a populated list into a heap (in-place)
heapq.heapify(alist)
```

## Functions

- To **access** the smallest item without popping it, use `heap[0]`.

- `heapq.heappush(<heap>, <item>)`

  Push the value *item* onto the *heap*, maintaining the heap invariant.

- `heapq.heappop(<heap>)`

  Pop and return the **smallest** item from the *heap*, maintaining the heap invariant. If the heap is empty, [`IndexError`](https://docs.python.org/2/library/exceptions.html#exceptions.IndexError) is raised.

- `heapq.heappushpop(heap, item)`

  Push *item* on the heap, then pop and return the **smallest** item from the *heap*. The combined action runs more efficiently than [`heappush()`](https://docs.python.org/2/library/heapq.html#heapq.heappush) followed by a separate call to [`heappop()`](https://docs.python.org/2/library/heapq.html#heapq.heappop).

- `heapq.heapreplace(heap, item)`

  Pop and return the **smallest** item from the *heap*, and also push the new *item*. The heap size doesn’t change. If the heap is empty, [`IndexError`](https://docs.python.org/2/library/exceptions.html#exceptions.IndexError) is raised. This one step operation is more efficient than a [`heappop()`](https://docs.python.org/2/library/heapq.html#heapq.heappop) followed by [`heappush()`](https://docs.python.org/2/library/heapq.html#heapq.heappush) and can be more appropriate when using a fixed-size heap.

  The pop/push combination always returns an element from the heap and replaces it with *item*.The value returned may be larger than the *item* added. If that isn’t desired, consider using [`heappushpop()`](https://docs.python.org/2/library/heapq.html#heapq.heappushpop) instead. Its push/pop combination returns the smaller of the two values, leaving the larger value on the heap.

### General Purpose Functions

- `heapq.merge(*iterables)`

  Merge multiple sorted inputs into a single sorted output (for example, merge timestamped entries from multiple log files). Returns an [iterator](https://docs.python.org/2/glossary.html#term-iterator) over the sorted values.

- `heapq.nlargest(n, iterable[, key])`

  Return a list with the *n* **largest** elements from the dataset defined by *iterable*. *key*, if provided, specifies a function of one argument that is used to extract a comparison key from each element in the iterable: `key=str.lower`

- `heapq.nsmallest(n, iterable[, key])`

  Return a list with the *n* **smallest** elements from the dataset defined by *iterable*. *key*, if provided, specifies a function of one argument that is used to extract a comparison key from each element in the iterable: `key=str.lower`

