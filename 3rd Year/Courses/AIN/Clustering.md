# Clustering
Tag: #review 

---
## Definitions

---
## Notes

### Clustering
#### K-Means & K-Median

- K-Means minimises the Euclidean/Geometric distance
- K-Medians minimises the Manhattan distance

##### K-Means
This is a method of vector quantization that aims to partition n observations into K clusters.

K-means minimises within cluster variances and tends to find clusters of comparable spatial extent.

###### Steps
1. Select K cluster centres arbitrarily
2. Repeat until convergence
	1. Assign each point to the cluster with the nearest mean
	2. ![[Pasted image 20221108195050.png]][4] where each point is assigned to exactly one cluster $S_i$
	3. Update Step
		1. Recalculate the mean point of the cluster
		2. ![[Pasted image 20221108195208.png]][4]

##### K-Means ++

K-Means++ aims to solve the problem in K-Means where if we start with sub-optimal clusters and never change them , they can be made arbitrarily bad.

K-Means++ uses an approximation factor to fix this.

###### Steps
1. Set the first centre to be one of the input points chosen uniformly at random i.e. ![[Pasted image 20221108195512.png]][4]
2. For cluster i = 2 to k:
	1. For each point $X_j$ compute the distance to the nearest centre
	2. Open a new centre at a point using the weighted probability distribution that is proportional to $d_{j}^{2}$ ![[Pasted image 20221108195654.png]][4]
	3. Continue with k-Means

##### K-Median
K-Median is a variation of [[Machine Learning#K-Means|K-Means]] where instead of calculating the mean for each cluster to determine its centroid, one instead calculates the median.

#### Hierarchical Clustering
 We can choose K by using the Elbow method![[Pasted image 20221108201246.png]][2]

The problem with Clustering is that it can be quite flat, instead we can use Hierarchical Clustering.

This is the recursive partitioning of data at increasingly finer granularity represented as a tree
The leaves of the hierarchical cluster tree represent data
![[Pasted image 20221108201519.png]][2]

##### Agglomerative Clustering
An edge can mean similarity or dissimilarity

A high similarity value means that the corresponding two nodes are very similar and should be in the same cluster


###### Steps
1. Initially place each data point in its own clusters
2. Repeatedly merge most similar clusters

![[Pasted image 20221108201714.png]]![[Pasted image 20221108201748.png]][3]

###### Divisive Heuristics
1. Find a partition of the input similarity graph (or set of points)
	1. Split using bisection k-means
	2. Split using sparsest cut
2. Recurse on each part
3. Builds cluster-tree top-down

###### Sparsest Cut

Given a graph with nodes V and edges E

The sparsity of a cut is given by![[Pasted image 20221108201955.png]][3]

The sparsest cut of a graph is given by the S* that minimises the sparsity of a cut![[Pasted image 20221108202042.png]][3]


#### Dasgupta's Cost Function

Input: A weighted similarity graph G 
Output: T a tree with leaves labelled by nodes of G

Cost of the output: Sum of the costs of the nodes of T
Cost of a node N of the tree:![[Pasted image 20221108202739.png]][4]

Intuition: Better to cut a high similarity edge at a lower level

##### Recursive Sparsest Cut 

Dissimilarity graph: ![[Pasted image 20221108202912.png]][4]



 

---
## Footnotes
Backlink: [[Machine Learning]]

Sources:
1. 
	- Name: k-Means
	- Author: Frederik Mallmann-Trenn
	- Date: 08/11/22
2. 
	- Name: Hierarchical Clustering
	- Author: Frederik Mallmann-Trenn
	- Date: 08/11/22
3. 
	- Name: Hierarchical Clustering
	- Author: Frederik Mallmann-Trenn
	- Date: 08/11/22
4. 
	- Name: Hierarchical Clustering Objective
	- Author: Frederik Mallmann-Trenn
	- Date: 08/11/22