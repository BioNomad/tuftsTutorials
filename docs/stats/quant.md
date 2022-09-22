# Quantitative Variables

Quantitaive variables are numerical data: so variables such as height, weight, age. We can describe these variables with the following terms:


- **Minimum** 
- **Median**
- **Mean**
- **Max**
- **Count**
- **Standard deviation**

Let's see how to do this in our code:

```R
library(tidyverse)
meta <- read.table("./data/gbm_cptac_2021/data_clinical_patient.txt",
                     header = T,
                   sep="\t")

height.sum <- meta %>%
  summarise( 
    minimum = min(HEIGHT, na.rm = T),
    median = median(HEIGHT, na.rm = T),
    mean = mean(HEIGHT, na.rm = T),
    max = max(HEIGHT, na.rm = T),
    count = length(HEIGHT[!is.na(HEIGHT)]),
    SD = sd(HEIGHT, na.rm = T))

height.sum
```

```
  minimum median     mean max count       SD
1     150    170 169.6768 196    99 9.875581
```
