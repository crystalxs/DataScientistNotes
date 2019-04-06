#Running Time

>When code going slow, how could we check which part of the code costly?

Python includes a profiler called [cProfile](https://docs.python.org/3/library/profile.html). It not only gives the total running time, but also times each function separately, and tells you how many times each function was called, making it easy to determine where you should make optimizations.

You can call it from within your code, or from the interpreter, like this:

```text
import cProfile
cProfile.run('foo()')
```

Even more usefully, you can invoke the cProfile when running a script:

```text
python -m cProfile myscript.py
```

Running Time

