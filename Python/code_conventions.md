# Code Conventions

---
description: >-
  Using a consistent style provides better code management, readability,
  understandability, and maintenance. Here we mostly talk about PEP8.
---

# Code Conventions

## PEP8

### Check PEP8 programmatically

```text
pip install pycodestyle
pycodestyle your_code.py
```

#### Check \(autopep8\) on Jupyter Notebook:

```text
conda install -c conda-forge jupyter_contrib_nbextensions
jupyter contrib nbextension install --user  # Copy the nbextensions’ javascript and css files into the jupyter server’s search directory, and edits jupyter config files. ‘—user’ to install into the user’s home jupyter directories.
jupyter nbextensions_configurator enable    # Enable nbextension on Jupyter
conda install -c conda-forge autopep8       # Install autopep8 which comes with pycodestyle
```

### Code layout

* **Max line length:** 79 characters;
* **Continued lines:** long lines should be broken over multiple lines.
* **Indentation:** Use a tab \(4 spaces\) per indentation level
* **Blanklines:**

  Surround top-level function and class definitions with two blank lines;

  Method definitions inside a class are surrounded by a single blank line;

* **Importing libraries/packages:**

  Imports are always put at the top of the file;

  Imports should usually be on separate lines;

  Imports should be grouped in the following order and you should place a line between each group:

  * standard library imports
  * related third party imports
  * user defined modules imports

### Whitespace

* **No whitespace:**
  * Immediately inside parentheses, brackets or braces;
  * Between a trailing comma and a following close parenthesis;
  * Immediately before a comma, semicolon, or colon;

    _However, in a slice the colon acts like a binary operator, and should have equal amounts on either side_
* **Surround the following binary operators with a single space on either side:**

  * assignment \(=\), augmented assignment \(+=, -= etc.\), comparisons \(==, &lt;, &gt;, !=, &lt;&gt;, &lt;=, &gt;=, in, not in, is, is not\), Booleans \(and, or, not\)
* **If operators with different priorities are used, consider adding whitespace around the operators with the lowest priority\(ies\);**
* **Don't use spaces around the = sign when it is used to assign a keyword argument or a default parameter value;**
* **Multiple statements on the same line are discouraged.**

### Comments

* **Comments should be complete sentences written in English;**
* **Block comments:** Block comments generally consist of one or more paragraphs built out of complete sentences, with each sentence ending in a period
  * Each line of a block comment starts with a \# and a single space;
  * block comments are indented to the same level as that code;
* **In line comments:** An inline comment is a comment on the same line as a statement
  * Inline comments should be separated by at least two spaces from the statement;
  * They should start with a \# and a single space;
  * Use inline comments sparingly;
* **Docstring:** Describe the operation of the function or class, docstrings will be shown in an interactive Python session when you type `help(module.function)`
  * Use triple double quotes `"""` around docstrings;
  * Write docstrings for all public modules, functions, classes, and methods;
  * For one line docstrings, keep the closing `"""` on the same line;
  * The `"""` that ends a multiline docstring should be on a line by itself.

### Naming Conventions

* **Naming styles:**
  * b \(single lowercase letter\) – Never use 'l' \(lowercase letter el\), 'O' \(uppercase letter oh\), or 'I' \(uppercase letter eye\).
  * B \(single uppercase letter\)
  * lowercase, lower\_case\_with\_underscores
  * UPPERCASE, UPPER\_CASE\_WITH\_UNDERSCORES
  * CapitalizedWords \(or CapWords, or CamelCase\)
  * mixedCase
  * \_single\_leading\_underscore: weak "internal use" indicator. \(won’t be imported.\)
* **Packages and modules:**
  * Packages: Packages should have short, all-lowercase names, although the use of underscores is discouraged.
  * Modules: Modules should have short, all-lowercase names. Underscores can be used in the name.
* **Function and variables:**
  * Function names: should be lowercase, with words separated by underscores.
  * Variable names: follow the same convention as function names.