---
title: "Multivariate Analysis"
subtitle: "Practice"
author: "Joyce Jin"
output:  
  html_document:
    keep_md: true
---





# Question 1: PCO
In a psychology experiment from the 1950s, Ekman (1954) asked 31 subjects to rank the similarities of 14 different colors. His goal was to understand the underlying dimensionality of color perception. The similarity or confusion matrix was scaled to have values between 0 and 1. The ekman.csv similarity matrix can be found at :
The colors that were often confused had similarities close to 1. Colours are encoded as wxxx, where xxx is the wavelength in nm

Convert the ekman data into a dissimilarity matrix (Pay attention to the diagonal).

Use PCO to analyse the dissimilarity matrix you just created and:

(i) show the eigenvalue-screeplot, and

(ii) plot the first two dimensions of the scores of the PCO analysis.

```r
ekman.dat<-read.csv("https://raw.githubusercontent.com/mpawley001/323/main/ekman.csv")
```


```r
summary(ekman.dat)
```

```
##       w434             w445             w465             w472       
##  Min.   :0.0000   Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
##  1st Qu.:0.0625   1st Qu.:0.0700   1st Qu.:0.0200   1st Qu.:0.0125  
##  Median :0.1050   Median :0.1000   Median :0.0650   Median :0.0650  
##  Mean   :0.1886   Mean   :0.1971   Mean   :0.1921   Mean   :0.1964  
##  3rd Qu.:0.1750   3rd Qu.:0.2000   3rd Qu.:0.3575   3rd Qu.:0.3775  
##  Max.   :0.8600   Max.   :0.8600   Max.   :0.8100   Max.   :0.8100  
##       w490             w504             w537             w555       
##  Min.   :0.0000   Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
##  1st Qu.:0.0200   1st Qu.:0.0200   1st Qu.:0.0275   1st Qu.:0.0325  
##  Median :0.1250   Median :0.0850   Median :0.0850   Median :0.0750  
##  Mean   :0.1950   Mean   :0.1814   Mean   :0.1750   Mean   :0.1679  
##  3rd Qu.:0.2975   3rd Qu.:0.2300   3rd Qu.:0.2000   3rd Qu.:0.2425  
##  Max.   :0.6100   Max.   :0.6200   Max.   :0.7300   Max.   :0.7300  
##       w584             w600             w610             w628       
##  Min.   :0.0000   Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
##  1st Qu.:0.0200   1st Qu.:0.0250   1st Qu.:0.0200   1st Qu.:0.0125  
##  Median :0.1700   Median :0.1100   Median :0.0600   Median :0.0700  
##  Mean   :0.1779   Mean   :0.2193   Mean   :0.2393   Mean   :0.2421  
##  3rd Qu.:0.2600   3rd Qu.:0.3775   3rd Qu.:0.5050   3rd Qu.:0.4425  
##  Max.   :0.5800   Max.   :0.7400   Max.   :0.7600   Max.   :0.8500  
##       w651             w674       
##  Min.   :0.0000   Min.   :0.0000  
##  1st Qu.:0.0200   1st Qu.:0.0125  
##  Median :0.0900   Median :0.0900  
##  Mean   :0.2321   Mean   :0.2071  
##  3rd Qu.:0.3575   3rd Qu.:0.2675  
##  Max.   :0.8500   Max.   :0.7600
```


```r
ekman.dat
```

```
##    w434 w445 w465 w472 w490 w504 w537 w555 w584 w600 w610 w628 w651 w674
## 1  0.00 0.86 0.42 0.42 0.18 0.06 0.07 0.04 0.02 0.07 0.09 0.12 0.13 0.16
## 2  0.86 0.00 0.50 0.44 0.22 0.09 0.07 0.07 0.02 0.04 0.07 0.11 0.13 0.14
## 3  0.42 0.50 0.00 0.81 0.47 0.17 0.10 0.08 0.02 0.01 0.02 0.01 0.05 0.03
## 4  0.42 0.44 0.81 0.00 0.54 0.25 0.10 0.09 0.02 0.01 0.00 0.01 0.02 0.04
## 5  0.18 0.22 0.47 0.54 0.00 0.61 0.31 0.26 0.07 0.02 0.02 0.01 0.02 0.00
## 6  0.06 0.09 0.17 0.25 0.61 0.00 0.62 0.45 0.14 0.08 0.02 0.02 0.02 0.01
## 7  0.07 0.07 0.10 0.10 0.31 0.62 0.00 0.73 0.22 0.14 0.05 0.02 0.02 0.00
## 8  0.04 0.07 0.08 0.09 0.26 0.45 0.73 0.00 0.33 0.19 0.04 0.03 0.02 0.02
## 9  0.02 0.02 0.02 0.02 0.07 0.14 0.22 0.33 0.00 0.58 0.37 0.27 0.20 0.23
## 10 0.07 0.04 0.01 0.01 0.02 0.08 0.14 0.19 0.58 0.00 0.74 0.50 0.41 0.28
## 11 0.09 0.07 0.02 0.00 0.02 0.02 0.05 0.04 0.37 0.74 0.00 0.76 0.62 0.55
## 12 0.12 0.11 0.01 0.01 0.01 0.02 0.02 0.03 0.27 0.50 0.76 0.00 0.85 0.68
## 13 0.13 0.13 0.05 0.02 0.02 0.02 0.02 0.02 0.20 0.41 0.62 0.85 0.00 0.76
## 14 0.16 0.14 0.03 0.04 0.00 0.01 0.00 0.02 0.23 0.28 0.55 0.68 0.76 0.00
```
Convert the ekman data into a dissimilarity matrix (Pay attention to the diagonal).

```r
# Convert the data frame 'ekman.dat' to a matrix
similarity_matrix <- as.matrix(ekman.dat)

# Subtract the similarity_matrix from 1 to create the dissimilarity_matrix
dissimilarity_matrix <- 1 - similarity_matrix

# Set the diagonal elements of the dissimilarity_matrix to 0
diag(dissimilarity_matrix) <- 0
```

Show dissimilarity_matrix

```r
dissimilarity_matrix 
```

```
##       w434 w445 w465 w472 w490 w504 w537 w555 w584 w600 w610 w628 w651 w674
##  [1,] 0.00 0.14 0.58 0.58 0.82 0.94 0.93 0.96 0.98 0.93 0.91 0.88 0.87 0.84
##  [2,] 0.14 0.00 0.50 0.56 0.78 0.91 0.93 0.93 0.98 0.96 0.93 0.89 0.87 0.86
##  [3,] 0.58 0.50 0.00 0.19 0.53 0.83 0.90 0.92 0.98 0.99 0.98 0.99 0.95 0.97
##  [4,] 0.58 0.56 0.19 0.00 0.46 0.75 0.90 0.91 0.98 0.99 1.00 0.99 0.98 0.96
##  [5,] 0.82 0.78 0.53 0.46 0.00 0.39 0.69 0.74 0.93 0.98 0.98 0.99 0.98 1.00
##  [6,] 0.94 0.91 0.83 0.75 0.39 0.00 0.38 0.55 0.86 0.92 0.98 0.98 0.98 0.99
##  [7,] 0.93 0.93 0.90 0.90 0.69 0.38 0.00 0.27 0.78 0.86 0.95 0.98 0.98 1.00
##  [8,] 0.96 0.93 0.92 0.91 0.74 0.55 0.27 0.00 0.67 0.81 0.96 0.97 0.98 0.98
##  [9,] 0.98 0.98 0.98 0.98 0.93 0.86 0.78 0.67 0.00 0.42 0.63 0.73 0.80 0.77
## [10,] 0.93 0.96 0.99 0.99 0.98 0.92 0.86 0.81 0.42 0.00 0.26 0.50 0.59 0.72
## [11,] 0.91 0.93 0.98 1.00 0.98 0.98 0.95 0.96 0.63 0.26 0.00 0.24 0.38 0.45
## [12,] 0.88 0.89 0.99 0.99 0.99 0.98 0.98 0.97 0.73 0.50 0.24 0.00 0.15 0.32
## [13,] 0.87 0.87 0.95 0.98 0.98 0.98 0.98 0.98 0.80 0.59 0.38 0.15 0.00 0.24
## [14,] 0.84 0.86 0.97 0.96 1.00 0.99 1.00 0.98 0.77 0.72 0.45 0.32 0.24 0.00
```
Use PCO to analyse the dissimilarity matrix you just created and:
(i) show the eigenvalue-screeplot, and

(ii) plot the first two dimensions of the scores of the PCO analysis.

```r
# Perform PCoA
n <- dim(dissimilarity_matrix)[1]
PCO <- cmdscale(dissimilarity_matrix, k = (n - 1), eig = TRUE)
```

```
## Warning in cmdscale(dissimilarity_matrix, k = (n - 1), eig = TRUE): only 12 of
## the first 13 eigenvalues are > 0
```
Scree plot


```r
# Extract the eigenvalues
eig_values <- PCO$eig

# Calculate the proportion of variance explained by each dimension
variance_explained <- eig_values / sum(eig_values)

# Create a scree plot using the base plot function
plot(variance_explained, type = "b", xlab = "Dimension", ylab = "Proportion of Variance Explained",
     main = "Scree Plot for PCoA Eigenvalues")
```

![](README_figs/README-unnamed-chunk-7-1.png)<!-- -->

Score

```r
# Extract eigenvalues and calculate the percentage of variance explained
lambda2 <- PCO$eig
round(100 * lambda2 / sum(lambda2), digits = 2)
```

```
##  [1] 45.25 29.66 10.06  8.54  3.62  2.35  0.95  0.72  0.42  0.10  0.03  0.00
## [13] -0.61 -1.08
```

```r
# Create a new data frame containing the first two PCoA axes
pco_dat <- data.frame(PCO1 = PCO$points[, 1], PCO2 = PCO$points[, 2])

# Plot the data using ggplot2
library(ggplot2)
p_pco <- ggplot(pco_dat, aes(x = PCO1, y = PCO2)) + geom_point() + ggtitle("PCoA Plot")
print(p_pco)
```

![](README_figs/README-unnamed-chunk-8-1.png)<!-- -->



# Question 2: nMDs

Changes in the community of organisms living in Waiwera estuary has been assessed by the Auckland Regional Council to determine the impact of housing developments. The data from a few sampling sites are held in :

The 1st variable Site should be stored as a factor since it is just a label (either 2, 4, 6 or 8), the remaining 146 variables are counts of the animals found in each replicate taken at one of the sample sites.

```r
Waiwera.dat<-read.csv("https://raw.githubusercontent.com/mpawley001/323/main/WaiweraEstData.csv")
Waiwera.dat[1:5,1:6]
```

```
##   Rain Site Aglmac Alphsp Amaaus Ampcre
## 1    D    2      0      0      0      0
## 2    D    2      0      0      0      0
## 3    D    2      0      0      0      0
## 4    D    2      0      0      0      0
## 5    D    2      0      0      0      0
```

```r
dim(Waiwera.dat)
```

```
## [1]  48 147
```

Answer the items below:

(i) Produce a non-metric MDS using Bray-Curtis (BC) distance to visualize benthic fauna collected from sediment samples in the Waiwera estuary. (Use can calculate BC distance using wither the my.dist function code used int he lab, or by using the `vegan::vegdist()` function).

```r
library(vegan)
```

```
## Loading required package: permute
```

```
## This is vegan 2.6-4
```

```r
# Calculate Bray-Curtis distance
bc_dist <- vegdist(Waiwera.dat[,3:147], method = "bray")

# Perform NMDS
nmds <- metaMDS(bc_dist, distance = "bray", k = 2)
```

```
## Run 0 stress 0.1641462 
## Run 1 stress 0.1938111 
## Run 2 stress 0.1641463 
## ... Procrustes: rmse 5.094822e-05  max resid 0.0003183469 
## ... Similar to previous best
## Run 3 stress 0.2156247 
## Run 4 stress 0.1938499 
## Run 5 stress 0.177837 
## Run 6 stress 0.1958028 
## Run 7 stress 0.1905089 
## Run 8 stress 0.1777466 
## Run 9 stress 0.1639172 
## ... New best solution
## ... Procrustes: rmse 0.01077927  max resid 0.04261492 
## Run 10 stress 0.1641459 
## ... Procrustes: rmse 0.0106286  max resid 0.04278632 
## Run 11 stress 0.1785621 
## Run 12 stress 0.1962966 
## Run 13 stress 0.2007968 
## Run 14 stress 0.163933 
## ... Procrustes: rmse 0.005138145  max resid 0.02071101 
## Run 15 stress 0.1777475 
## Run 16 stress 0.1778595 
## Run 17 stress 0.1641578 
## ... Procrustes: rmse 0.009131104  max resid 0.04440953 
## Run 18 stress 0.1748161 
## Run 19 stress 0.163918 
## ... Procrustes: rmse 0.0003789221  max resid 0.002362316 
## ... Similar to previous best
## Run 20 stress 0.1972113 
## *** Best solution repeated 1 times
```

```r
# Extract NMDS scores
nmds_scores <- data.frame(Site = Waiwera.dat$Site, NMDS1 = nmds$points[, 1], NMDS2 = nmds$points[, 2])

# Visualize NMDS plot
ggplot(nmds_scores, aes(x = NMDS1, y = NMDS2, color = as.factor(Site))) +
  geom_point(size = 3) +
  labs(color = "Site") +
  ggtitle("Non-metric MDS (Bray-Curtis) for Waiwera Estuary Data") +
  theme_minimal()
```

![](README_figs/README-unnamed-chunk-11-1.png)<!-- -->


```r
nmds$stress
```

```
## [1] 0.1639172
```
The stress is 0.16, which is smaller than 0.2. Consider it's good.


(ii) Create the associated Shepard plot of the Waiwera estuarine data (based on the same Bray-Curtis distances).


```r
stressplot(nmds)
```

![](README_figs/README-unnamed-chunk-13-1.png)<!-- -->


```r
Stress <- c(1:10)
for(i in 1:10) {
  Stress[i]  <-  metaMDSiter(vegdist(Waiwera.dat[,3:147], method="bray"), k = i,trace = FALSE)$stress
}
plot(Stress)
```

![](README_figs/README-unnamed-chunk-14-1.png)<!-- -->



# Question 3: K-means clutsering of USArrests data

In this question, we will use the built-in R data set USArrests, which contains statistics from 1973 in arrests per 100,000 residents for: Assault, Murder, and Rape as well as the percent of the population living in urban areas (UrbanPop). There are seven (4) short items, to answer in this question.

```r
data("USArrests")
```

As we don’t want the clustering algorithm to depend to an arbitrary variable unit, standardize the data using the R function scale().

Use a Euclidean distance and visualize the distance matrix using the function get_dist() and fviz_dist() from the factoextra package.


```r
USArrests
```

```
##                Murder Assault UrbanPop Rape
## Alabama          13.2     236       58 21.2
## Alaska           10.0     263       48 44.5
## Arizona           8.1     294       80 31.0
## Arkansas          8.8     190       50 19.5
## California        9.0     276       91 40.6
## Colorado          7.9     204       78 38.7
## Connecticut       3.3     110       77 11.1
## Delaware          5.9     238       72 15.8
## Florida          15.4     335       80 31.9
## Georgia          17.4     211       60 25.8
## Hawaii            5.3      46       83 20.2
## Idaho             2.6     120       54 14.2
## Illinois         10.4     249       83 24.0
## Indiana           7.2     113       65 21.0
## Iowa              2.2      56       57 11.3
## Kansas            6.0     115       66 18.0
## Kentucky          9.7     109       52 16.3
## Louisiana        15.4     249       66 22.2
## Maine             2.1      83       51  7.8
## Maryland         11.3     300       67 27.8
## Massachusetts     4.4     149       85 16.3
## Michigan         12.1     255       74 35.1
## Minnesota         2.7      72       66 14.9
## Mississippi      16.1     259       44 17.1
## Missouri          9.0     178       70 28.2
## Montana           6.0     109       53 16.4
## Nebraska          4.3     102       62 16.5
## Nevada           12.2     252       81 46.0
## New Hampshire     2.1      57       56  9.5
## New Jersey        7.4     159       89 18.8
## New Mexico       11.4     285       70 32.1
## New York         11.1     254       86 26.1
## North Carolina   13.0     337       45 16.1
## North Dakota      0.8      45       44  7.3
## Ohio              7.3     120       75 21.4
## Oklahoma          6.6     151       68 20.0
## Oregon            4.9     159       67 29.3
## Pennsylvania      6.3     106       72 14.9
## Rhode Island      3.4     174       87  8.3
## South Carolina   14.4     279       48 22.5
## South Dakota      3.8      86       45 12.8
## Tennessee        13.2     188       59 26.9
## Texas            12.7     201       80 25.5
## Utah              3.2     120       80 22.9
## Vermont           2.2      48       32 11.2
## Virginia          8.5     156       63 20.7
## Washington        4.0     145       73 26.2
## West Virginia     5.7      81       39  9.3
## Wisconsin         2.6      53       66 10.8
## Wyoming           6.8     161       60 15.6
```

```r
dim(USArrests)
```

```
## [1] 50  4
```

```r
# Load libraries
library(factoextra)
```

```
## Welcome! Want to learn more? See two factoextra-related books at https://goo.gl/ve3WBa
```

```r
library(cluster)
library(gridExtra)

# Scale the data
scaled_USArrests <- scale(USArrests)

# Calculate Euclidean distance
dist_matrix <- get_dist(scaled_USArrests)

# Visualize distance matrix
fviz_dist(dist_matrix)
```

![](README_figs/README-unnamed-chunk-18-1.png)<!-- -->


Answer the items below:
1. From your distance matrix visualization, can you get a feel for any clusters? If so, which states appear to be be fairly similar to each other?
*From the distance matrix visualization, it's difficult to identify clear clusters.However, there are some regions with similar colors, which indicate similar distances. For example, New York and Illinois; Nevada and vermont *


2. Calculate a k-means solutions for 2 clusters. Visualize the clustering results using the function: fviz_cluster().


```r
# K-means clustering with 2 clusters
kmeans_2 <- kmeans(scaled_USArrests, centers = 2)

# Visualize clustering results
fviz_cluster(kmeans_2, data = scaled_USArrests)
```

![](README_figs/README-unnamed-chunk-19-1.png)<!-- -->

3. Repeat step 2 choosing different numbers of clusters (k=3, 4 and 5). Use the gridExtra:grid.arrange() function to plot the ordinations in a 2x2 grid.


```r
# K-means clustering with 3, 4, and 5 clusters
kmeans_3 <- kmeans(scaled_USArrests, centers = 3)
kmeans_4 <- kmeans(scaled_USArrests, centers = 4)
kmeans_5 <- kmeans(scaled_USArrests, centers = 5)

# Visualize clustering results
viz_2 <- fviz_cluster(kmeans_2, data = scaled_USArrests)
viz_3 <- fviz_cluster(kmeans_3, data = scaled_USArrests)
viz_4 <- fviz_cluster(kmeans_4, data = scaled_USArrests)
viz_5 <- fviz_cluster(kmeans_5, data = scaled_USArrests)

# Display visualizations in a 2x2 grid
grid.arrange(viz_2, viz_3, viz_4, viz_5, nrow = 2)
```

![](README_figs/README-unnamed-chunk-20-1.png)<!-- -->


4. Use fviz_nbclust to create a Scree plot using the Within Group Sum-of-Squares as your criterion. Use the elbow method to choose the number of clusters (justify your choice from the plot).



```r
# Determine the optimal number of clusters using the elbow method
fviz_nbclust(scaled_USArrests, kmeans, method = "wss")
```

![](README_figs/README-unnamed-chunk-21-1.png)<!-- -->


The within-cluster sum of squares (wss) experiences a sharp decline from 1 to 4 clusters. However, beyond this point, the decrease in wss slows down, and surprisingly, there's an increase when it moves to 5 clusters. Therefore, considering this pattern, I select 4 as the appropriate number of clusters for the data. 







