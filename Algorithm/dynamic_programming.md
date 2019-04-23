# Dynamic Programming

Caching or memorizing partial results and using those to avoid redundant computation.

1. Identify a collection of subproblems;
2. Solve subproblems one by one, working from smallest to largest;
3. Use the answers to the smaller problems to help solve the larger ones.

## Memoized recursive

```python
def f(input):
  # check termination condition
  # return memoized result if possible
  # process the active input region
  # invoke f on subregions
  # combine results and memoize
  # return results
```