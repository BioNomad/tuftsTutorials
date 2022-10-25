## Clustering

Clustering, like the name implies, is a way to group data points to find patterns. Clustering is type of unsupervised learning - where patterns are discovered without labeled data. 

## Distance Metrics

Before generating clusters we need to calculate the distance between observations. To do so we have a few options:

$$Euclidean\ Distance = d_{euc}(x,y) = \sqrt{\sum_{i=1}^n{(x_i - y_i)^2}}$$

!!! example "Explanation of Terms"
    - $x$ variable x
    - $y$ variable y
    - $n$ number of observations
    
$$Manhattan\ Distance = d_{man}(x,y) = \sum_{i=1}^n{|(x_i - y_i)|}$$

!!! example "Explanation of Terms"
    - $x$ variable x
    - $y$ variable y
    - $n$ number of observations
    
$$Eisen\ Cosine\ Correlation\ Distance  = d_{eis}(x,y) = 1 - \frac{|\sum_{i=1}^n{x_iy_i}|}{\sqrt{\sum_{i=1}^n {x_i^2}\sum_{i=1}^n {y_i^2}}}$$

!!! example "Explanation of Terms"
    - $x$ variable x
    - $y$ variable y
    - $n$ number of observations
    
$$Pearson\ Correlation\ Distance = d_{pearson}(x,y) = 1 - \frac{\sum_{i=1}^n{(x - \mu_x)(y - \mu_y)}}{\sqrt{\sum_{i=1}^n{(x - \mu_x)^2} \sum_{i=1}^n{(y - \mu_y)^2}}} $$

!!! example "Explanation of Terms"
    - $x$ variable x
    - $y$ variable y
    - $\mu_x$ mean of variable x
    - $\mu_y$ mean of variable y
    - $n$ number of observations
    
$$Spearman\ Correlation\ Distance = d_{spearman}(x,y) = 1 - \frac{\sum{(x\prime - \mu_{x\prime} )(y\prime  - \mu_{y\prime} )}}{\sqrt{\sum{(x\prime  - \mu_{x\prime} )^2} \sum{(y\prime  - \mu_{y\prime} )^2}}}$$

!!! example "Explanation of Terms"
    - $x$ variable x
    - $y$ variable y
    - $\mu_x$ mean of variable x
    - $\mu_y$ mean of variable y
    - $n$ number of observations

## K-means Clustering 

## Agglomerative Hierarchical Clustering

## References
