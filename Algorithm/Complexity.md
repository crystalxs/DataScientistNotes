# Time Complexity

## Unit of work

comparisions

floating-point operations

visiting nodes

traversing edges

swapping array elements

......

## Defination

$T(n)$ = total operations required to operate on size n

$O(n)$ = ignore constants and only keep most important terms

| **f(n)**   | **Name**    |
| :--------- | :---------- |
| 11         | Constant    |
| lognlog⁡n   | Logarithmic |
| nn         | Linear      |
| nlognnlog⁡n | Log Linear  |
| n2n2       | Quadratic   |
| n3n3       | Cubic       |
| 2n2n       | Exponential |

## Process

1. identify what we are counting as a unit of work
2. identify the key indicator of problem size
   * usually size n
   * for $n \times m$, claim worst-case that n is bigger, thus $n \times n$
3. define $T(n)$, then solve sum or recurrence for closed form
4. define $O(n)$

