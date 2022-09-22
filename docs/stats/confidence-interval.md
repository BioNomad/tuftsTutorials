## Confidence Intervals

Estimating the mean from a sample is going to have some fluctuation defined by the standard error. We can define a range or **confidence interval** 
which we expect to contain the true mean. Often we report a 95% confidence interval. This interval is defined by plus or minus two times the standard error:

$$ -2\frac{\sigma}{\sqrt{N}} \le \mu  \le +2\frac{\sigma}{\sqrt{N}}$$

- $\sigma$ Standard deviation of the sample
- $N$ Number of observations in the sample
- $\mu$ sample mean

Let's try this with our sample:

```R
library(tidyverse)
# load meta data
meta <- read.table("./data/gbm_cptac_2021/data_clinical_patient.txt",
                   header = T,
                   sep="\t")

## defined some population of ages
ages <- sample(meta$AGE,20)

## data frame of results
summary <- data.frame(
  Sample_Mean=mean(ages,na.rm = T),
  Standard_Error=sd(ages,na.rm = T)/sqrt(length(ages[!is.na(ages)])),
  Lower_Bound_CI = mean(ages,na.rm = T) - 2*(sd(ages,na.rm = T)/sqrt(length(ages[!is.na(ages)]))),
  Upper_Bound_CI = mean(ages,na.rm = T) + 2*(sd(ages,na.rm = T)/sqrt(length(ages[!is.na(ages)])))
)

summary

```

```
  Sample_Mean Standard_Error Lower_Bound_CI Upper_Bound_CI
1        55.2       3.701778       47.79644       62.60356
```

!!! note
    So we are 95% confident that the true mean lies somewhere between `47.79644` and `62.60356`

## References

- [BIOL202 Tutorials](https://ubco-biology.github.io/BIOL202/desc_cat_Var.html)
