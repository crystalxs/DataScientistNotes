# R markdown

MacTex is required for RMarkdown pdf output.

### The header

begins and ends with three dashes `---`.

```text
---
title: "My Title"
auther: "Crystal"
date:
output: pdf_document
---
```

### Code Chunks

```text
```{r <sectionTitle>, <options>}
<include code here>
```
```

Using `ctrl` + `option` + `I` as keyboard shortcut to include code chunk.

&lt;sectionTitle&gt; is the unique name of the code chunk.

&lt;options&gt; are a sequence of options separated by commas.

All labels and code chunk options must be on the same line.

#### Options

`eval = F`: prevents code from being evaluated

`echo = F`: prevents code, but not results, from appearing in final output document

`include = F`: runs code but doesn’t show code or results in final output document

`message = F` / `warning = F`: prevents messages or warning from appearing in final output document

`cache = T`: will store the results of a code chunk in cache, so subsequent knits of the document don’t need to re-execute computationally expensive code chunks \(use only for static data\)

#### Global chunk options

```text
```{r <sectionTitle>, include = FALSE}
knitr::opts_chunk$set(<options>)
```
```

