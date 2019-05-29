# Recursion

**Recursion** is a method of solving problems that involves breaking a problem down into smaller and smaller subproblems until you get to a small enough problem that it can be solved trivially. Usually recursion involves a function calling itself.

```python
def f():
  f()
```

Algorithms that use a single recursive are easy to convert to loops, and loops are usually more efficient.

## Formula for recursive

1. A recursive algorithm must have a **base case**.
2. A recursive algorithm must change its state and move toward the base case.
3. A recursive algorithm must call itself, recursively.

```python
def f(input):
  # 1. check termination condition
  # 2. process the active input region
  # 3. invoke f on subregions
  # 4. combine and return result
```

## Complexity

The cost of any recursive algorithms depends on:

* the number of recursive subproblem calls per active region;
* the size of the subproblems;
* the work required for each active region.

##Divide and Conquer

1. Break a big problem down into smaller subproblems via recursion;
2. until subproblems are so small we can solve in constant time;
3. merge partial results in linear time as you climb back up the recursive calls.

* Divide and Conquer algorithm make 2 or more recursive calls;
* Each subproblem is a fraction of the size of the currently active problem.