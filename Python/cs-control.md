# Control Structures

## Iterations

### While

```python
while condition:
    operations
```

#### do-while

```python
while True:
  	operations
    if condition: break
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

The condition after the  `if` statement is a [boolean expression](cs-data.md/#Python built-in atomic data type).

```python
if condition:
    operations
else:
    operations
```

## List comprehension

```python
[expression for item in list]
[expression for item in list if conditional]
```

