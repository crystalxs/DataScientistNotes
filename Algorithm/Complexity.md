# Time Complexity

## Unit of Computation

comparisions

floating-point operations

visiting nodes

traversing edges

swapping array elements

## Defination

$T(n)$ = total operations required to operate on size n

$O(n)$ = ignore constants and only keep most important terms

| **f(n)** | **Name**    |
| :------- | :---------- |
| $1$      | Constant    |
| $logn$   | Logarithmic |
| $n$      | Linear      |
| $nlogn$  | Log Linear  |
| $n^2$    | Quadratic   |
| $n^3$    | Cubic       |
| $2^n$    | Exponential |

![../_images/newplot.png](/Users/crystal/Library/Mobile Documents/com~apple~CloudDocs/dataScientistNotes/Algorithm/image/complexity_O.png)

## Process

1. identify what we are counting as a unit of work
2. identify the key indicator of problem size
   * usually size n
   * for $n \times m$, claim worst-case that n is bigger, thus $n \times n$
3. define $T(n)$, then solve sum or recurrence for closed form
4. define $O(n)$

### Tips

* Careful recursive

  | **Recurrence**                 | **Complexity** | **Scenario**                                                 |
  | ------------------------------ | -------------- | ------------------------------------------------------------ |
  | $T(n) = 1 + T(n-1) = n$        | $O(n)$         | Process one item;<br />then rest                             |
  | $T(n) = n + T(n-1) = n^2/2$    | $O(n^2)$       | Looping through all *n*   items; <br />eliminating one from consideration each iteration or nested loops |
  | $T(n) = 1 + T(n/2) = log n$    | $O(log n)$     | Cut amount of work in half each iteration;<br />doing 1 operation |
  | $T(n) = n + T(n/2) = 2n$       | $O(n)$         | Cut amount of work in half each iteration;<br />but examine *n* items |
  | $T(n) = n + 2T(n/2) = n log n$ | $O(n log n)$   | Divide and conquer algorithms:<br />Cut amount of work in half each iteration;<br />but process both halves;<br />the combine results in linear time. |

* Careful of loop iteration step size

## Time vs Space

* Space complexity measures the amount of storage necessary to execute an algorithm as a function of input size;
* Time complexity measures the amount of time necessary to execute an algorithm as a function of input size;
* There is often a trade-off between using more memory and increasing speed.