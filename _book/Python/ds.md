# Data Type and Data Structure

## Data Type

### Boolean



### Numbers

### Strings

### Lists

### Sets



## Data Structure

### Dictionaries

“associative memories” or “associative arrays”

Dictionary indexed by *keys* (**unique**), can be any immutable type, numbers, strings, tuples (only contain numbers and strings).

#### Statement

```python
mydict = {}
mydict = dict()
# dict() can build directly from sequences of key-value pairs
```

#### Access

```python
d.keys()		# return keys of d 
d.itmes()		# return values of d
d.vales()		# return (key, value) of d

d[key]			# return the item of d with key
d.get(key)
d.pop(key)	# return and remove the item of d with key
d.popitem()	# return and remove a (key, value) pair, in LIFO order
```

#### Insert & update

```python
d[key] = value
d.update(key=value)
```

#### Delete

```python
del d[key]	# remove key in d
d.clear()		# remove all items in d
```

#### Other

```python
list(d)	# list of all keys
key in d	# check if key exist
key not in d
iter(d)	# iter the keys in d
d.copy	# shallow copy
```



