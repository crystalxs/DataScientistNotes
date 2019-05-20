# Hash Table

## Set

- unique and unordered list;
- typical implementation is a hash table;

#### Python

`set` in python.

#### Operations

add, delete, contains, union, intersection

contains: take constant time for hash table implementation

## Dictionary

Arrange two lists side-by-side and kind of glue them together, map one value to another.

### Time Complexity for python built-in `dict`

| operation     | Big-O Efficiency |
| :------------ | :--------------- |
| copy          | O(n)             |
| get item      | O(1)             |
| set item      | O(1)             |
| delete item   | O(1)             |
| contains (in) | O(1)             |
| iteration     | O(n)             |

### Python

`dict` in python.

## Hash Table

Array of linked lists / buckets and a hash code function.

1. Compute hash code by **hash function**
2. Map the hash code to an index in the array, which bucket.

### Time Complexity

Access: cannot access by index

Search: `O(1)` vs `O(n)`

- With a uniform distribution, we would expect roughly *N*/*B* associations in each bucket for *B* buckets and *N* total elements in the dictionary.
- A complexity of *N*/*B* is much better than *N* and, with sufficiently large *B*, we would say that *N*/*B* approaches 1, giving complexity *O(1)* versus *O(n)*.

Insert: `O(1)` vs `O(n)`

Delete: `O(1)` vs `O(n)`

### Hash Function

#### Remainder Method

`h(item)=item%11`

Magic Number: 31

#### Folding Method

1. Dividing the item into equal-size pieces (the last piece may not be of equal size);
2. Then added together to give the resulting hash value;
3. Apply remainder method.

#### Mid-square Method

1. Square the item;
2. Then extract some portion of the resulting digits;
3. Apply remainder method.