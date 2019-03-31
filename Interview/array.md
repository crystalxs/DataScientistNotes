# Array

####Methods

* Multi-pointers from begin and end or even med, in `python` commonly use index to be the pointer.
* [Hash table](Interview/hash.md)

#### Questions Classify

- sort
- duplicate (use hash table)

####Attention

- Boundary Check
  - Out of index
  - Ending points
- Length Check
  - Length = 0
  - Length = 1 (usually boundary)
  - Length = 2 (will decrease time complexity when using recursive)
- **Python specific attention**
  - Start index 0
  - Modify the array will change index
    - Do not delete element in array!!! Find another way
  - Array index=-1 is not out of range
  - Pay attention to shadow copy
- Two arrays
  - Check the length equal or not, exist or not

#### Leetcode

1. **Two Sum:** visit array

4. **Median of two sorted arrays:** divide and conquer
   * on target rather than array

11. **Container with most water:** two pointers

26. **Remove duplicates from sorted array:** two pointers
    * don't `pop` or `delete` element
    * exchange the position of unique element to front

55. **Jump Game:** bottom-up dynamic programming
    * use another array to record status
    * recursive will cost toooooo much

81. **Search in rotated sorted array:** binary search

189. **Rotate Array:** 
     * ideas: reverse twice / cyclic replacement / extra array

289. **Game of Life:** general visit matrix
     * make a copy to avoid change influence future