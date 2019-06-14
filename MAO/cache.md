# Cache

> Cache algorithms (also frequently called **cache replacement algorithms** or **cache replacement policies**) are optimizing instructions, or algorithms, that a computer program or a hardware-maintained structure can utilize in order to manage a cache of information stored on the computer. Caching improves performance by keeping recent or often-used data items in memory locations that are faster or computationally cheaper to access than normal memory stores. When the cache is full, the algorithm must choose which items to discard to make room for the new ones.

## Policy

### First in first out (FIFO)

> Evicts the first block accessed first without any regard to how often or how many times it was accessed before.

### Last in first out (LIFO)

> Evicts the block accessed most recently first without any regard to how often or how many times it was accessed before.

### Least recently used (LRU)

> Discards the least recently used items first.

