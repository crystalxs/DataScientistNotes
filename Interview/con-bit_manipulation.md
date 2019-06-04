# Bit Manipulation

## Bitwise Operators

**NOT ( ~ ):** (unary) Flips the bits of the number.

```python
~1 = 0
~0 = 1
```

**AND ( & ):** (binary) If both bits in the compared position of the bit patterns are 1, the bit in the resulting bit pattern is 1, otherwise 0.

```python
1&0 = 0
0&0 = 0
1&1 = 1
```

**OR ( | ):** (binary) If both bits in the compared position of the bit patterns are 0, the bit in the resulting bit pattern is 0, otherwise 1.

```python
1&0 = 1
0&0 = 0
1&1 = 1
```

**XOR ( ^ ):** (binary) If both bits in the compared position of the bit patterns are 0 or 1, the bit in the resulting bit pattern is 0, otherwise 1.

```python
1&0 = 1
0&0 = 0
1&1 = 1
```

**Left Shift ( << ):** (unary) In the given bit pattern, to the left and append **0** at the end.

**Right Shift ( >> ):** (unary)

- Logical: in the given bit pattern, to the left and append **sign bit** at the begin.
- Arithmetic: in the given bit pattern, to the left and append **0** at the most significant bit.

## Two Complement

**Positive Number:** N-bit number is the complement of the number with respect to $2^N$.

**Negative Number:** N-bit number represent for -K is $concat(1, 2^{N-1}-K)$:

1. Represent the positive number;
2. Invert the bits;
3. Add 1;
4. Prepend the sign bit 1.

## Tricks

| xor         | and         | or          |
| ----------- | ----------- | ----------- |
| `x^0s = x`  | `x&0s = 0s` | `x|0s = x`  |
| `x^1s = ~x` | `x&1s = x`  | `x|1s = 1s` |
| `x^x = 0s`  | `x&x = x`   | `x|x = x`   |



- If you XOR a bit with its own negated value, you will always get 1.



#### Methods

- `dict` in python
- Implemented in array and string for problem solving

#### Questions Classify

- Duplicate

#### Attention

- Could use `tuple` as key

#### Leetcode

136. **Single Number:** find duplicate
137. **Valid Anagram:** 2 hash table as map
138. **Contains Duplicate:** find duplicate
139. **Group Anagrams:** hash table with `tuple` as key
140. **Happy Number:** while loop & use hash table to get `o(1)` search
141. **Isomorphic String:** 2 hash table as map
142. **Repeated DNA Sequences:** find duplicate