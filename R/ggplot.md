---
description: Work only on data frame
---

# ggplot

#### Syntax 

`ggplot(data = <mydata>) + <geom_*>(mapping = aes(<myPreferredMapping>))`

```text
library(tidyverse)
library(magrittr)

<myData> %>%
  ggplot() +
  <geom_*>(mapping = aes(<myPreferredMapping>))
```

### Geoms

Geometric objects, or `geoms` as they are commonly known and used, describe the type of object used to display the data.

#### Common one-dimensional geoms:

`geom_histogram`

`geom_freqpoly`

`geom_density`

`geom_bar`

#### Common two-dimensional geoms:

`geom_point`

`geom_boxplot`

`geom_path` \(line in any direction\)

`geom_line` \(line from left to right\)

`geom_smooth` \(smoothed line with standard error\)

