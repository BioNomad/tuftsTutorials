# Sampling

When we try to assess an underlying population we often take samples of that population. Let's try and take a sample using the `sample()` function in R:

```R
## defined some population of ages
ages <- 3:110
sample <- sample(ages,n=20)
```

If we wanted to take the same random sample we could use the `set.seed()` function:

```R
## grab the same sample
set.seed(123)
sample1 <- sample(ages,n=20)
sample2 <- sample(ages,n=20)
```

## Sampling Error

Not every sample is going to be a true approximation of the underline population. This difference is known as the sampling error.
What's assess our sample and see how it stacks up against our population:

```R
data.frame(
Sample_Mean=mean(sample)
Population_Mean=mean(ages)
)
```

```R
```

We can calculate this differenceUsing the following formula:

$$\frac{\sigma}{\sqrt{N}}$$

- $\sigma$ Standard deviation of the sample
- $N$ Number of observations in the sample

So we can see that increasing the size of the sample, decreases the standard error of the mean.
