## One-Sample T-Test

When we deal with numeric variables we often examine the mean of that variable. The one-sample t-test can help answer the following questions about our 
numeric variable:

- **Does the mean of our sample, $\mu$, equal the theoretical mean of our population, $\mu_0$?**
    - $H_0: \mu = \mu_0$
    - $H_a: \mu \neq \mu_0$
- **Is the mean of our sample, $\mu$, less than the theoretical mean of our population, $\mu_0$?**
    - $H_0: \mu \le \mu_0$
    - $H_a: \mu > \mu_0$
- **Is the mean of our sample, $\mu$, greater than the theoretical mean of our population, $\mu_0$?**
    - $H_0: \mu \ge \mu_0$
    - $H_a: \mu  \mu_0$

!!! tip
    When we ask if the sample mean is equal to the population mean we are conducting a **two-sided test**. When we ask if the sample mean is less than 
    or greater than the population mean, we are conducting a **one-sided test**.

## Test Statistic

Our one-sample t-test statistic can be calculated by:

$$t = \frac{\mu - \mu_0}{\sigma / \sqrt{n}} $$

$$d.f. = n - 1$$

!!! example "Explanation of Terms"
    - $\mu$ : sample mean
    - $\mu_0$ : theoretical population mean
    - $\sigma$ : standard deviation of our sample
    - $n$ : sample size
    - $d.f.$ : degrees of freedom

## Normal Distribution

Using our glioblastoma data, we are going to ask: Does the mean age of our patients equal the theoretical mean of the U.S. population (Let's say the avearage age is 32)? Before we do so, we need to ask; what probability function are we comparing our test statistic to? For a numeric variable we often compare our test statistic to a Gaussian or normal distribution. The probability density function for the normal distribution has the following formula:

$$f(x) = \frac{1}{(\sigma\sqrt{2 \pi})} e^{-(\frac{(x - \mu)^2}{2 \sigma^2})}$$

!!! example "Explanation of Terms"
    - $\sigma$ : standard deviation
    - $\mu$ : mean

## Confidence Interval

Just like our proportion tests, we also have a confidence interval around our sample parameter, in this case the sample mean. So for a test statistic, $t$, at an $\alpha$ level of 0.05, our confidence interval would be:

$$\mu \pm t \frac{\sigma}{\sqrt{n}}$$

!!! example "Explanation of Terms"
    - $\mu$ : sample mean
    - $t$ : test statistic for an $\alpha$ of 0.05
    - $\sigma$ : sample standard deviation
    - $n$ :  sample size

## Running the One-Sample T-Test

Putting this all together let's test whether or not the mean of our sample is equal to the theoretical mean of our population, 32:

```R
#one-sample t-test
library(tidyverse)
# load meta data
meta <- read.table("./data/gbm_cptac_2021/data_clinical_patient.txt",
                   header = T,
                   sep="\t")

# run the one-sample t-test to determine if the
# mean of our sample is equal to 32
t.test(x = meta$AGE,
       mu = 32,
       alternative = "two.sided")
```

```
	One Sample t-test

data:  meta$AGE
t = {==20.621, df = 98, p-value < 2.2e-16==}
{==alternative hypothesis: true mean is not equal to 32==}
95 percent confidence interval:
 {==55.39750 60.38028==}
sample estimates:
mean of x 
 {==57.88889==} 
```

!!! info "Explanation"
    - our test statistic is `20.621`
    - our d.f. is `98`
    - The pvalue is below `2.2e-16`
    - our alternative hypothesis is that the true mean is not equal to 32
    - our sample mean is `57.88889` 
    - the 95% confidence interval for our mean is `55.39750` to `60.38028`
    - So we see that we have enough evidence to reject the null hypothesis that the true mean of our sample is equal to 32
    
## Assumptions

So now that we have conducted our test, we should assess the test's assumptions:

- the values are independent of one another
- the numeric variable is a continuous numeric variable
- there are no signficant outliers
- the data are normally distributed

## References

1. [BIOL 202 - One-Sample T-Test](https://ubco-biology.github.io/BIOL202/onesamp_t_test.html)
2. [One-Sample T-test in R](http://www.sthda.com/english/wiki/one-sample-t-test-in-r)
3. [Normal Distribution](https://en.wikipedia.org/wiki/Normal_distribution)
