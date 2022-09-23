## Estimating Proportions

When we estimate proportions using a sample, this proportion is also subject to sampling error. And just like the mean, we can estimate it's standard error with:

$$SE_p = \sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$$

!!! example "Term Definitions"
    - $SE_p$ standard error of the proportion
    - $\hat{p}$ sample proportion
    - $n$ number of observations
    - $X$ number of successes out of $n$ observations (down below)
    
However, there is an issue with this standard error estimate: When either the $n$ is small or our $\hat{p}$ is extreme (close to 0 or 1) the estimate is not reliable. To remedy this we use the Agresti-Coull interval:

$$p^\prime = \frac{X + 2}{n + 4}$$

So that the confidence interval is:

$$1.96 \pm \sqrt{\frac{p^\prime(1-p^\prime)}{n + 4}}$$



## Binomial Distribution

## Hypothesis Testing

## References

1. [Wilson score and Agresti-Coull intervals for binomial proportions](https://statisticaloddsandends.wordpress.com/2019/06/09/wilson-score-and-agresti-coull-intervals-for-binomial-proportions/)
2. [BIOL - 202: Analyzing a single categorical variable](https://ubco-biology.github.io/BIOL202/estproportions.html)
