# Data Structure

## 146. LRU Cache

```python
class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = {}
        self.used = []

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        else:
            self.used.remove(key)
            self.used.append(key)
            return self.cache[key]

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.used.remove(key)
        else:
            if len(self.cache) >= self.capacity:
                popkey = self.used.pop(0)
                self.cache.pop(popkey)
        self.cache[key] = value
        self.used.append(key)

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

