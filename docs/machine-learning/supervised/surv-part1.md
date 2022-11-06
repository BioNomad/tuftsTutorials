## Survival Analysis Part 1

Survival Analysis refers to a statistical framework to assess the time it takes for some event of interest to occur. In medical research this framework
is often used to ask questions about:

- a patient's probability of survival given some time period
- the characteristics that might impact survival
- the differences in survival between groups

## Events and Censoring

The type of event can include:

- Relapse
- Death 
- Progression

Now not all patients in a study will experience the same type of event described above and as such these observations need to be *censored* as to not 
influence our results. Censoring can be caused by:

- a patient not yet experiencing an event of interest (Relapse, Death, Progression, etc.)
- a patient being lost to follow up during the study (meaning they drop out for one reason or another)
- a patient expreiences an alternative event to the event of interest

Given that these are assessed at the end of the study, this is referred to as **right censoring**.

## Kaplan-Meier Survival Probability

The probability that the event of interest **will not happen** in a given time period is referred to as the survival probability. We can calculate this
using the non-parametric Kaplan-Meier method:

$$S(t_i) = S({t_i} - 1) (1 - \frac{d_i}{n_i})$$

$$S(0) = 1$$

$$t_0 = 0$$

!!! example "Explanation of Terms"

    - $S(t_i)$ Survival probability at time $t_i$
    - $S({t_i} - 1)$ Survival probability at time ${t_i} - 1$
    - $n_i$ number of patients that have not experienced event of interest right before time $t_i$
    - $d_i$ number of events of interest at $t_i$
    - $t_0 = 0$ your starting time must be 0
    - $S(0) = 1$ your probability of survival at time 0 is 1 
    
## Pre-Processing

Let's start by loading our meta data and ensuring that we have a censored column:

```R
# load the libraries
.libPaths(c("/cluster/tufts/hpc/tools/R/4.0.0"))
library("survival")
library("survminer")

# load in patient meta data
meta <- read.csv(
  file = "data/gbm_cptac_2021/data_clinical_patient.txt",
  skip=4,
  header = T,
  sep = "\t"
)

# create a censored status column
# 1 being they are censored
# 2 being they are not censored
meta$status <- ifelse(
  (meta$LOST_TO_FOLLOW_UP == "Yes" & meta$VITAL_STATUS == "Living"),
  1,
  2
)

```

## References

1. [Survival Analysis Basics](http://www.sthda.com/english/wiki/survival-analysis-basics)
2. [Survival Analysis Part I: Basic concepts and first analyses](https://www.nature.com/articles/6601118)
3. [Nonparametric Estimation from Incomplete Observations](https://www.jstor.org/stable/2281868#metadata_info_tab_contents)
4. [Survival plots of time-to-event outcomes in clinical trials: good practice and pitfalls](https://www.sciencedirect.com/science/article/pii/S014067360208594X?via%3Dihub)
