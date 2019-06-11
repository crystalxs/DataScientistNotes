# collections

> https://docs.python.org/2/library/collections.html#collections.defaultdict

This module implements specialized container datatypes providing alternatives to Python’s general purpose built-in containers, [`dict`](https://docs.python.org/2/library/stdtypes.html#dict), `list`, [`set`](https://docs.python.org/2/library/stdtypes.html#set), and [`tuple`](https://docs.python.org/2/library/functions.html#tuple).

## `defaultdict`

> Dict subclass that calls a factory function to supply missing values.

When each key is encountered for the first time, it is not already in the mapping; so an entry is automatically created using the `default_factory` function which returns an empty <value-data-type>.

If the key doesn't exist in the dict, it won't return error, instead, it will return an empty <value-data-type>.

### Declaration

`defaultdict(<value-data-type>)`

## `counter`

> Dict subclass for counting hashable objects.

### Declaration

```python
c = Counter()                           # a new, empty counter
c = Counter('gallahad')                 # a new counter from an iterable
c = Counter({'red': 4, 'blue': 2})      # a new counter from a mapping
c = Counter(cats=4, dogs=8)             # a new counter from keyword args
```

### Methods

* `del c[element]`: remove an element from a counter;
* `elements()`: return an iterator over elements repeating each as many times as its count, elements are returned in arbitrary order. If an element’s count is less than one, `elements()` will ignore it;
* `most_common([n])`: return a list of the *n* most common elements and their counts from the most common to the least. If *n* is omitted or `None`, returns all elements in the counter, elements with equal counts are ordered arbitrarily;
* `subtract()`: elements are subtracted from an *iterable* or from another *mapping* (or counter);
* `update()`: elements are counted from an *iterable* or added-in from another *mapping* (or counter). Like [`dict.update()`](https://docs.python.org/2/library/stdtypes.html#dict.update) but adds counts instead of replacing them. Also, the *iterable* is expected to be a sequence of elements, not a sequence of `(key, value)` pairs.

| [`namedtuple()`](https://docs.python.org/2/library/collections.html#collections.namedtuple) | factory function for creating tuple subclasses with named fields | *New in version 2.6.* |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------- |
| [`deque`](https://docs.python.org/2/library/collections.html#collections.deque) | list-like container with fast appends and pops on either end | *New in version 2.4.* |
| [`Counter`](https://docs.python.org/2/library/collections.html#collections.Counter) | dict subclass for counting hashable objects                  | *New in version 2.7.* |
| [`OrderedDict`](https://docs.python.org/2/library/collections.html#collections.OrderedDict) | dict subclass that remembers the order entries were added    | *New in version 2.7.* |
| [`defaultdict`](https://docs.python.org/2/library/collections.html#collections.defaultdict) |                                                              | *New in version 2.5.* |