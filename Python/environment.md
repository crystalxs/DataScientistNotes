# Environment

---
description: "Keep dependencies required by different projects\_in\_separate\_places;  Easily switch to a environment that requires different dependencies."
---

# Environment

### Create an environment

```text
conda create --name MSDS694 python=3.6 -y
```

`-y`: yes to all the questions

#### Creating using .yml

```text
conda env create -f MSDS694_environment.yml -n MSDS694
```

#### Checking available environments

```text
conda info --envs
```

![](.gitbook/assets/image.png)

`*`means where the current environment is.

`base` is the default environment.

### Activate the environment

```text
source activate MSDS694
```

### Deactivate the environment

```text
source deactivate
```

### Check available environments and the current environment

```text
conda info --envs
```

### Export the environment file

Using to share and reproduce the environments including all the packages with corresponding versions.

```text
conda env export > MSDS694_environment.yml
```

`.yml`: Data serialization language. Commonly used for configuration files.

### Update an environment using .yml

```text
conda env update –f MSDS694_environment.yml –n MSDS694
```

Stored in current directory

### Remove the environment

```text
conda remove --name MSDS694 --all
```

`--all` make sure to remove all the dependencies.