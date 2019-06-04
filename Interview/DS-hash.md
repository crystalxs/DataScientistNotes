# Hash table

#### Methods

- `dict` in python
- Implemented in array and string for problem solving

#### Questions Classify

- Duplicate

#### Attention

- Could use `tuple` as key

## Leetcode

136. **Single Number:** find duplicate
137. **Valid Anagram:** 2 hash table as map
138. **Contains Duplicate:** find duplicate
139. **Group Anagrams:** hash table with `tuple` as key
140. **Happy Number:** while loop & use hash table to get `o(1)` search
141. **Isomorphic String:** 2 hash table as map
142. **Repeated DNA Sequences:** find duplicate

### 1. Two Sum

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        sumNums = {}
        
        for index, num in enumerate(nums):
            if num in sumNums:
                return [index, sumNums[num]]
            else:
                sumNums[target-num] = index
```