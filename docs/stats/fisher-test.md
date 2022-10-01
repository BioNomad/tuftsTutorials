## Fisher's Exact Test

In the [odds ratio topic note](odds-ratio-risk.md) we noted that the odds ratio could help us determine whether the odds 
were greater in one group versus another. We can test the strength of association of the group and event with **Fisher's Exact Test**. 
Fisher's Exact Test has the following hypotheses:

- $H_0$ or null hypothesis: there is no association between the group and event (Odds ratio = 1)
- $H_a$ or alternative hypothesis: there is an association between the group and event (Odds ratio != 1)

Let's assess the relationship between females and losing patients to follow up:

```R
library(tidyverse)
# load meta data
meta <- read.table("./data/gbm_cptac_2021/data_clinical_patient.txt",
                   header = T,
                   sep="\t")

# What is the frequency distribution of losing males/females to follow up
table <- as.data.frame.matrix(
  table(meta$SEX,meta$LOST_TO_FOLLOW_UP)
)

table
```

```
       No Yes
Female 33  10
Male   44  10
```

!!! danger 
    Before we continue, note that the first columns is not losing patients to follow up!
    If we want to test for the event of **losing** patients to follow up we need to put the "Yes", or Patients lost to follow up, column first.
    
```R
# Reorder so that we are assessing the odds ratio of losing patients to follow up
table <- as.data.frame.matrix(
  table(meta$SEX,meta$LOST_TO_FOLLOW_UP)
) %>%
  select(c(Yes,No))

table
```

```
       Yes No
Female  10 33
Male    10 44
```

Now let's conduct our hypothesis test:

```R
#apply our test
fisher.test(table)
```

```
	Fisher's Exact Test for Count Data

data:  table
p-value = {==0.6191==}
alternative hypothesis: true odds ratio is not equal to 1
95 percent confidence interval:
 {==0.4395952 4.0274603==}
sample estimates:
odds ratio 
   {==1.32933==} 
```

!!! info "Explanation of Results"
    Here we note:
    - our p-value is above 0.05 and thus not strong enough to reject the null (a.k.a the true odds ratio is equal to 1)
    - the 95% confidence interval reveals that our true odds ratio is somewhere between `0.4395952` and `4.0274603`
    - our odds ratio that patient sex is associated with losing the patient to follow up is about `1.3`

## References

1.[BIOL 202](https://ubco-biology.github.io/BIOL202/fishertest.html)
