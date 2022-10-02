## Chi-Square Test

When comparing categorical variables, your data won't always have 2x2 dimensions as in the [Fisher's Test Topic Note](fisher-test.md). 
For tables with greater dimensions we can use the Chi-square test to test hypotheses of association. 
The Chi-Square or $\chi^2$ test is defined by:

$$\chi^2 = \sum_i{\frac{(O_i-E_i)^2}{E_i}}$$

with:

$$d.f. = (r-1)(c-1)$$

!!! example "Explanation of Terms"
    
    - $\chi^2$ chi-square statistic
    - $O_i$ observed value at cell i
    - $E_i$ expected value at cell i
    - $d.f.$ degrees of freedom
    - $r$ number of rows
    - $c$ number of columns
    
This $\chi^2$ value is then compared to a probability distriubtion. In our [Binomial Test Topic Note](binomial-test.md), we described that 
probability distributions help us determine the probability of an event given some parameter. In the [Binomial Test Topic Note](binomial-test.md),
that parameter was the number of successes, but here it is our degrees of freedom. We won't cover the math of this probability distribution function
here, but if your curious check out [the wikipedia page on chi-sqare distributions](https://en.wikipedia.org/wiki/Chi-squared_distribution). 
Let's use R to examine how probability changes with varying degrees of freedom and $\chi^2$ values:

```R
# examine the chi square cdf
chi.sq.df <- data.frame(
  probability = 0,
  chi_square = 0,
  df = 0
)
for(i in 2:9){
  chi.sq.df.i <- data.frame(
    probability = dchisq(1:10,i),
    chi_square = 1:10,
    df = rep(as.character(i),10)
  )
  chi.sq.df <- rbind(chi.sq.df,
                     chi.sq.df.i)
}
chi.sq.df <- chi.sq.df[-1,]


ggplot(chi.sq.df,            
       aes(x = chi_square,
           y = probability,
           color = df)) +  
  geom_line()+
  theme_bw()
```

![](images/chi-square-dist.png)

Now, what you might have guessed from the equation above, but we are testing the following hypotheses:

- $H_0$ or null hypothesis that there is no association between the two categorical values
- $H_a$ or alternative hypothesis that there is an association between the two categorical values

Here we will test the association between losing a patient to follow up and their country of origin. Let's try visualizing this first:

```R
# load meta data
meta <- read.table("./data/gbm_cptac_2021/data_clinical_patient.txt",
                   header = T,
                   sep="\t")


# generate a table of losing a patient to follow up
# by their country of origin
# removing zero count countries
table <- as.data.frame.matrix(
  table(meta$LOST_TO_FOLLOW_UP,meta$COUNTRY_OF_ORIGIN)
) %>%
  select(c(China,Poland,Russia, `United States`))

#plot our data
table %>% 
  t() %>% 
  reshape2::melt() %>%
  ggplot(.,aes(x=Var1,y=value,fill=Var2))+
  geom_bar(stat = "identity",position="fill") +
  scale_y_continuous(labels = scales::percent)+
  theme_bw()+
  scale_fill_manual(values=c("aquamarine3","lightpink3")) +
  labs(
    x="",
    y="Frequency",
    fill="Lost To Follow Up?"
  )

```

![](images/chi-square-lost-to-follow.png)
