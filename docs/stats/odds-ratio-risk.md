## Risk

We have defined odds as the probability of that event happening divided by the probability of that event not happening. 
In our topic note on [odds](odds.md) we asked what were the odds of losing a male patient to follow up. This is different from **risk**.
Risk can be defined as:


$$Risk = \frac{n_i}{N}$$

!!! example "Explanation of Terms"
    - $n_i$ number of times event happened
    - $N$ total number of events
    
Here we see this is just a proportion or the number of times an event happened divided by the total number of events! Let's assess the risk of 
losing a male patient to follow up:

```R
#risk
library(tidyverse)
# load meta data
meta <- read.table("./data/gbm_cptac_2021/data_clinical_patient.txt",
                   header = T,
                   sep="\t")

# what are the odds of being a female non-smoker in our dataset?
table <- as.data.frame.matrix(
  table(meta$SEX,meta$LOST_TO_FOLLOW_UP)
) %>%
  mutate(row_totals = apply(.,1,sum)) %>%
  rbind(t(data.frame(column_totals=apply(., 2, sum))))

table


male <- table %>%
  filter(rownames(.) == "Male") %>%
  mutate(
    risk_male_lost = Yes/row_totals,
    risk_male_not_lost = No/row_totals)

male
```

```
     No Yes row_totals risk_male_lost risk_male_not_lost
Male 44  10         54      0.1851852          0.8148148
```

We see that the risk of losing a male patient to follow up is about 18%. 

## Relative Risk

You might hear about two risks how relate to each other - also called the **relative risk**. Relative risk can be calculated by:

$$Relative Risk = \frac{Risk_i}{Risk_j}$$

Where :

$$Risk_i = \frac{n_i}{N_i}$$

$$Risk_j = \frac{n_j}{N_j}$$

!!! example "Explanation of Terms"
    - $n_i$ number of times event i happened
    - $N_i$ total number of events when assessing event i
    - $n_j$ number of times event j happened
    - $N_j$ total number of events when assessing event j
    
    
So let's calculate the relative risk of losing a female patient to follow up versus a male patient:

```R
risks <- table %>%
  filter(rownames(.) != "column_totals") %>%
  mutate(
    risk_lost = Yes/row_totals,
    risk_not_lost = No/row_totals)

relative_risk <- risks$risk_lost["Female"]/risks$risk_lost["Male"]

relative_risk
```

```
  Female 
1.255814 
```

Here we see that risk of losing a female patient to follow up is greater than losing a male patient to follow up.
