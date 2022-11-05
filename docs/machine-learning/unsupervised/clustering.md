## Clustering

Clustering, like the name implies, is a way to group data points to find patterns. Clustering is type of unsupervised learning - where patterns are discovered without labeled data. 

## Distance Metrics

Before generating clusters we need to calculate the distance between observations:

![](images/calc_dist_mat.png)

To do so we have a few different options for distance metrics:

**Euclidean Distance**

$$d_{euc}(x,y) = \sqrt{\sum_{i=1}^n{(x_i - y_i)^2}}$$

!!! example "Explanation of Terms"
    - $x$ variable x
    - $y$ variable y
    - $n$ number of observations
    
**Manhattan Distance**

$$d_{man}(x,y) = \sum_{i=1}^n{|(x_i - y_i)|}$$

!!! example "Explanation of Terms"
    - $x$ variable x
    - $y$ variable y
    - $n$ number of observations
  
**Eisen Cosine Correlation Distance**

$$d_{eis}(x,y) = 1 - \frac{|\sum_{i=1}^n{x_iy_i}|}{\sqrt{\sum_{i=1}^n {x_i^2}\sum_{i=1}^n {y_i^2}}}$$

!!! example "Explanation of Terms"
    - $x$ variable x
    - $y$ variable y
    - $n$ number of observations
    
**Pearson Correlation Distance**  

$$d_{pearson}(x,y) = 1 - \frac{\sum_{i=1}^n{(x - \mu_x)(y - \mu_y)}}{\sqrt{\sum_{i=1}^n{(x - \mu_x)^2} \sum_{i=1}^n{(y - \mu_y)^2}}} $$

!!! example "Explanation of Terms"
    - $x$ variable x
    - $y$ variable y
    - $\mu_x$ mean of variable x
    - $\mu_y$ mean of variable y
    - $n$ number of observations

**Spearman Correlation Distance**  

$$d_{spearman}(x,y) = 1 - \frac{\sum{(x\prime - \mu_{x\prime} )(y\prime  - \mu_{y\prime} )}}{\sqrt{\sum{(x\prime  - \mu_{x\prime} )^2} \sum{(y\prime  - \mu_{y\prime} )^2}}}$$

!!! example "Explanation of Terms"
    - $x$ variable x
    - $y$ variable y
    - $\mu_x$ mean of variable x
    - $\mu_y$ mean of variable y
    - $n$ number of observations

## Distance Metrics In R

Let's try creating a distance matrix!

```R
# load the libraries
.libPaths(c("/cluster/tufts/hpc/tools/R/4.0.0"))
library(tidyverse)
library(factoextra)

# load our counts data
counts <- read.csv(
  file="data/gbm_cptac_2021/data_mrna_seq_fpkm.txt",
  header = T,
  sep = "\t")

# make the genes our rownames
rownames(counts) <- make.names(counts$Hugo_Symbol,unique = TRUE)

# remove the gene symbol column
counts <- counts %>%
  select(-c(Hugo_Symbol)) 

# log2 transform our data 
# transpose our data so that our patients are rows
counts <- t(log2(counts + 1))

# Change NA counts to 0
counts[!is.finite(counts)] <- 0

# generate correlation distance matrix
dist <- get_dist(counts,method = "pearson")

# plot correlation distance matrix
fviz_dist(dist) +
  theme(axis.text = element_text(size = 3)) +
  labs(
    title = "Pearson Correlation Distances Between Samples",
    fill = "Pearson Correlation"
  )
```

![](images/sample_corr_mat.png)

## K-means Clustering 

K-means clustering seeks to derive $k$ number of clusters so that the variation within the cluster is minimized. Additionally, the number of clusters, $k$, is specified by the user. The standard k-means algorithm is the Hartigan-Wong algorithm, which starts by determining the sum of squares for each cluster:

$$W(C_k) = \sum_{x_i\in{C_k}}{(x_i - \mu_k)^2}$$
    
Then the total within cluster variation is calculated by:

$$total\ within\ cluster\ variation = \sum_{k=1}^k{\sum_{x_i\in{C_k}}{(x_i - \mu_k)^2}}$$

!!! example "Explanation of Terms"

    - $C_k$ cluster number $k$
    - $x_i$ point in cluster $C_k$
    - $\mu_k$ mean of points in cluster $C_k$
    - $k$ number of clusters
    
!!! info
    This total within cluster variation is then minimized to best assign data points to the $k$ number of clusters
    
### Choosing $k$ Number of Clusters

In R we can use the `fviz_nbclust()` to determine the optimal number of clusters. This will generate a plot and where the plot dips dramatically is our optimal number of $k$!

```R
# k-means clustering
# choosing k
fviz_nbclust(counts, kmeans, method = "wss") +
  geom_point(color="midnightblue")+
  geom_line(color="midnightblue")+
  geom_vline(xintercept = 3,color="firebrick")
```

![](images/opt_k.png)

Here we do not see a drastic dip in our plot so we will choose 3 clusters here.

### Applying K-means

We will now perform k-means clustering and plot the results!

```R
# applying the k-means function
km <- kmeans(counts, 3, nstart = 25)
fviz_cluster(km, 
             counts,
             geom = "point",
             ellipse.type = "norm")+
  theme_bw()+
  labs(
    title = "K-means Cluster Plot with 3 Clusters"
  )
```

![](images/kmeans_plot.png)

You will note here that the clusters overlap to a great degree and there isn't great separation between them.

### K-means Shortcomings

Given the lackluster cluster plot above it is worth discussing the shortcomings of k-means clustering:

!!! warning "K-means Shortcomings"
    - you are going to need to determine the optimal number of clusters ahead of time
    - the initial center point is chosen at random! And as such your cluster can change depending on that random center point
    - this approach can rely heavily on the mean of the cluster points and the mean is sensitive to outliers in the data!
    - k-means clustering can be affected by data order as well
    

## Agglomerative Hierarchical Clustering

## References

1. [Clustering Distance Measures](https://www.datanovia.com/en/lessons/clustering-distance-measures/)
2. [K-Means Clustering in R: Algorithm and Practical Examples](https://www.datanovia.com/en/lessons/k-means-clustering-in-r-algorith-and-practical-examples/)
