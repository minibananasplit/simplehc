*This code is tested and run under the **R environment***

**Simple Hierarchical Cluster Analysis**

> Import Packages

```
library(tidyverse)  # data manipulation
library(cluster)    # clustering algorithms
library(factoextra) # clustering visualization
library(dendextend) # for comparing two dendrograms
```

>Hierarchical Clustering Algorithms

1) Agglomerative clustering (AGNES)
2) Divisive hierarchical clustering (DIANA) 

> Import Data
```
seven_matrix<-matrix(c(10,8,15,3,
	               21,15,21,6,
        	       8,8,10,4,
                       23,17,19,8,
                       12,9,10,3,
               	       13,10,9,3,
               	       9,6,7,4),nrow=7,byrow=T)
 
c("A","B","C","D","E","F","G")->row.names(seven_matrix)
c("Body_length","Tail_length","Wingspan","Beak_length")->colnames(seven_matrix)
```
> Hierarchical Clustering with R

***1) Agglomerative Hierarchical Clustering***
```
# Dissimilarity matrix
dist <- dist(seven_matrix, method = "euclidean")

# Hierarchical clustering using Complete Linkage
hc1 <- hclust(dist, method = "complete" )

# Plot the obtained dendrogram
plot(hc1, cex = 0.6, hang = -1)
plot(as.dendrogram(hc1),horiz=TRUE)
```
- Agnes

```
# Compute with agnes
hc2 <- agnes(dist, method = "complete")

# Agglomerative coefficient
hc2$ac
## [1] 0.8213396

## plot(as.dendrogram(hc2),horiz=TRUE)
```
- Ward's method indetifies

A) methods to assess
```
m <- c( "average", "single", "complete", "ward")
names(m) <- c( "average", "single", "complete", "ward")
```

B) function to compute coefficient
```
ac <- function(x) {
  agnes(dist, method = x)$ac
}

map_dbl(m, ac)
```
- Dendogram Visualization
```
hc3 <- agnes(dist, method = "ward")
pltree(hc3, cex = 0.6, hang = -1, main = "Dendrogram of agnes")
plot(as.dendrogram(hc3),horiz=TRUE)
```
***2) Divisive Hierarchical Clustering***

A) Compute divisive hierarchical clustering
```
hc4 <- diana(dist)
hc4$dc
[1] 0.8514345
```

B) Plot dendrogram
```
pltree(hc4, cex = 0.6, hang = -1, main = "Dendrogram of diana")
plot(as.dendrogram(hc4),horiz=TRUE)
```

>References
This source of code is from ***https://uc-r.github.io/hc_clustering*** with different my school assignment dataset
