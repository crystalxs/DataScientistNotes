# Control Structures

## Iterations

### While

```python
while condition:
    operation 1
    operation 2
    ...
```

### For

#### For-each Loop

The for-each loop *iterates* through a sequence of elements, such as a list but can be any iteratable object, such as a file on the disk. 

```python
for each x in sequence:
    operate on x
```

#### Indexed Loop

These are useful when we have to iterate through multiple lists at the same time. 

```python
for i in some integer_set or range:
    operation 1
    operation 2
    ...
```

####Zip'd Loop

Iterate through multiple lists at the same time without an indexed loop (using a for-each loop).

```python
for name, phone in zip(names,phones):
    print(f"{name:>8}: {phone}")
```

**If one tuple contains more items, these items are ignored.**

#### Combined Loop

```python
for i,row in enumerate(A):
    print(f"{i+1}. {row}")
```

## Selections - ifelse

```python
f condition:
    operation 1
    operation 2
    ...
else:
    operation 1
    operation 2
    ...
```

## List comprehension

```python
[ expression for item in list if conditional ]
```

