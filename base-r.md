---
description: Remember R is case sensitive.
---

# Base R

#### Help function

```text
?foo
??foo
RSiteResearch("foo")
```

```text
data()    # list all available datasets
getwd()   # list current working directory
setwd("~/Desktop")    # change working directory to Desktop
rm()      # Remove one or more object
ls()      # List object in the current directory
```

### Useful keyboard shortcut

`tab` Autocomplete

`cmd/ctrl` + `↑` history

`cmd/ctrl` + `enter` execute subset of code

`cmd/ctrl` + `shift` + `enter` execute subset of code

`cmd/ctrl` + `shift` + `F10` restarting an R session

### Clean environment

```text
rm(list=ls())    # remove all the objects in current environment
cat("\014")      # clear the console window
```

`ctrl` + `l` do the same thing as `cat("\014")` under mac.

### Packages

Only need to download a package once; however, always need to load packages when restarting an R session.

```text
library()    # show the packages are saved in your library (downloaded)
# show the packages are loaded and ready to use
(.packages())
search()
update.packages()                    # update all packages
installed.packages()                 # list all downloaded packages
install.packages("myPackageName")    # install package
library("myPackageName")             # load package into current working seesion
                                     # return an error if the package could not be loaded
require("myPackagaName")             # load package
                                     # throw a warning if the package could not be loaded
myPackageName::myFunctionName        # call a function from a specific package
detach("package:myPackagaName", unload = T)    # unload a package
```

When loading a package, it will automatically load their dependencies, however, when unload a package, it won't automatically unload the dependency that were loaded when we load that package.

#### Function masking

Because there are so many R packages available from so many different authors, it often happens that different packages have identically named functions.

### Logical Operations

| Operator | Descriptions |
| :--- | :--- |
| &lt; | less than |
| &lt;= | less than  or equal to |
| &gt; | greater than |
| &gt;= | greater than or equal to |
| == | exactly equal to |
| != | not equal to |
| ! x | not x |
| x \| y | x or y |
| x & y | x and y |
| isTRUE\(x\) | test if x is TRUE |

## Data Structure

| Dimension | Homogeneous | Heterogeneous |
| :--- | :--- | :--- |
| 1 | Atomic Vector | List |
| 2 | Matrix | Data Frame |
| n | Array |  |

There are no 0-dimmensional \(scalar\) types in R, only vectors of length one.

#### Check the length of a vector

`length()`

### Vector

The basic data structures in R: atomic vectors and lists.

`is.atomic()` and `is.list()` to determine if an object is a vector.

#### **Logical**

TRUE/FALSE, T/F

Not recognize True/False, should be all capitalized.

#### **Integer**

Create an integer vector:

```text
integerAtomicVector <- c(1L, 3L, 19L)
```

if without `L`, it will create double vector.

#### **Double \(numeric\)**

#### **Character**

#### Missing values

Missing values are specified with `NA`, which is a logical vector of length one.

`NA` will always be coerced to the correct type if used inside `c()`

You can create NAs of a specific type with:

* `NA_real_ (double)`
* `NA_integer_`
* `NA_character_`

`NA` and `NULL` are not the same.

 `na.rm = TRUE`

#### Check the type of a vector

`typeof()` and `class()`

More specifically:

`is.character()`, `is.double()`, `is.integer()`, `is.logical()`, `is.na()`

#### Assignment Operator `<-`

Using `Option (alt)` + `-` keyboard shortcut.

#### **Accessing elements of a vector**

```text
(myAtomicVector <- c(1, 2, 3, 4, -99, 5, NA, 4, 22.223))
myAtomicVector[5]
myAtomicVector[c(1, 2, 5, 9)]
myAtomicVector[10]
myAtomicVector[3:8]
```

#### Coercion

If you attempt to combine different types in an atomic vector they will be coerced to the most flexible type;

Most to least flexible types: character, double, integer, logical;

When a logical vector is coerced to numeric \(double or integer\): `TRUE = 1` and `FALSE = 0`

Explicitly coerce:

`as.character()`, `as.double()`, `as.integer()`, and `as.logical()`.

#### Brief Digression

`str()` and `tibble::glimpse()`

#### Subset an Atomic Vector

**Positive integers** return elements at the specified positions

```text
(myAtomicVector_01 <- c(99.1, 98.2, 97.3, 96.4))
myAtomicVector_01[c(1, 3)]
# 99.1 97.3
# real numbers are automatically truncated
myAtomicVector_01[c(1.999, 3.001)]
# 99.1 97.3
```

**Negative integers** omit elements at specified positions

```text
myAtomicVector_01[-c(1, 3)]
# 98.2 96.4
myAtomicVector_01[c(-1, -3)]
# 98.2 96.4
myAtomicVector_01[-c(-1, -3)]
# 99.1 97.3
myAtomicVector_01[c(-1,- 3.99)]
# 98.2 96.4
```

**Logical vectors** select elements where the logical value is TRUE

```text
myAtomicVector_01[c(TRUE, TRUE, FALSE, FALSE)]
# 99.1 98.2
myAtomicVector_01[c(T, TRUE, F, FALSE)]
# 99.1 98.2
```

If the logical vector is shorter than the vector being subsetted, it will be recycled to be the same length.

A missing value in the index always yields a missing value in the output.

**Character vectors** can can be employed to return elements with matching names if the vector is named.

Partial character string matches will not work

Conditionally

### List

Element of a list can be of any type, including list.

#### Constructed

`list()`

#### Functions

```text
is.list()    # test if list
as.list()    # coerce to list
unlist()     # convert to atomic vector + coercion
```



