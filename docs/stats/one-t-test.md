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
    
Our one-sample t-test statistic can be calculated by:

$$t = \frac{\mu - \mu_0}{\sigma / \sqrt{n}} $$

$$d.f. = n - 1$$

!!! example "Explanation of Terms"
    - $\mu$ : sample mean
    - $\mu_0$ : theoretical population mean
    - $\sigma$ : standard deviation of our sample
    - $n$ : sample size
    - $d.f.$ : degrees of freedom
    
