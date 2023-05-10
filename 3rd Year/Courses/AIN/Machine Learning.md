# Machine Learning
Tags: #review

---
## Definitions

---
## Notes
### PCA
##### PCA Example
Let’s say we have the following features
- Floor size pm2 q 
- Number of rooms
- Distance supermarket
- Distance King’s
- Hipster vibe
Let’s say we want to reduce to two features to have a nice visual representation.
Can we reduce it to two features?

Reduce to two or three features
- Size
	- Floor size m$^2$
	- Number of rooms
- Location
	- Distance supermarket
	- Distance King’s
	- Hipster vibe
![[Pasted image 20221027170140.png]]



For example the floor size and the number of rooms are often correlated.
We can compress both dimensions to one dimension.


![[Pasted image 20221027170358.png]][1]

If we take the line that minimises the Least Squares Distance, we get the following projection of the points.![[Pasted image 20221027170439.png]][1]
After cleaning this up, we get ![[Pasted image 20221027170518.png]][1]


Now if we take a different line, the spread here is the variance of the data![[Pasted image 20221027170551.png]][1]
If we would like to maximise it...
Intuitively, the more variance we capture, the better we can approximate the higher-dimensional space (here d “ 2)


![[Pasted image 20221027170654.png]][1]
If we compare them, we see that the points are less spread out on the purple line The black line actually maximises the spread and therefore is the best for approximating the higher-dimensional space

##### Why we maximise the variance
![[Pasted image 20221027170739.png]][1]
*Note: left is the new input and the right is two potential lines onto which we can project.*

Now lets try projecting a horizontal and vertical line![[Pasted image 20221027170840.png]][1]

As seen the black line retains more information.
So say we put this onto 3 dimensions.

Example:
($x_1,x_2,x_3$)![[Pasted image 20221027171110.png]][1]
- Distance Supermarket
- Distance King's
- Hipster Vibe
Then after reducing it to 2D it looks like this![[Pasted image 20221027171058.png]][1]

We may also wish to reduce it to just a line p1Dq, but we can see that this would be very lossy.

If we plot 5D data using the components we found (1 for size, 2 for location).
We get a well spread 3D plot![[Pasted image 20221027171219.png]][1]

This is the whole point!!
Reduce information but keep the important information.

##### Advantages
- State-of-the-art for many applications (supervised and unsupervised)
- Incredibly efficient (often, almost linear time)
- Strong theoretical background
- Can also be used to store data in more efficient way (Image compression)
- Visual evaluation possible for a small number of components (say 2)

#### Rotations & Eigenstuff
When a vector doesn't change its direction after multiplying with a matrix, then it's an **eigenvector**.

More importantly, the value that changes length is called the eigenvalue $λ$

The eigenvector for the matrix ![[Pasted image 20221027171659.png]][2] is![[Pasted image 20221027171718.png]][2]

##### Formula

The formula for an eigenvector is ![[Pasted image 20221027171754.png]][2]

$M$ = Matrix
$v$ = Vector
$λ$ = Eigenvalue 

**Example**
![[Pasted image 20221027171930.png]]![[Pasted image 20221027171946.png]]![[Pasted image 20221027172003.png]][2]

The second eigenvector is ![[Pasted image 20221027172027.png]][2]
Then $λ_2$ = -3

*Remember: if A·v=λ·v*

*Then (A·v)-(λ·v)=0*

#### PCA Algorithm

1. Compute the mean row vector ![[Pasted image 20221027173230.png]][3]
2. Compute the mean row matrix![[Pasted image 20221027173253.png]][3]
3. Subtract mean (obtain mean centred data)![[Pasted image 20221027173320.png]][3]
4. Compute the covariance matrix of rows of B![[Pasted image 20221027173346.png]][3]
5. Compute the k largest eigenvectors v$_1$, v$_1$, . . . , v$_k$ of C (You use Python or WolframAlpha). Each eigenvector has dimensions 1 x d
	*Python doesn’t sort the eigenvectors for you. Sort eigenvectors by decreasing order of eigenvalues*
6. Compute matrix W of k-largest eigenvectors![[Pasted image 20221027173513.png]][3]
7. Multiply each data-point x$_i$  for $_{i}\in$  {1, 2, … ,n} with W$^T$![[Pasted image 20221027173733.png]][3]

**Why compute the covariance matrix?**
The covariance matrix measures the correlation between pairs of features.
- Finding the largest eigenvectors allows us to explain most of the variance in data
- The more variance is explained by the eigenvectors, the more important they are
- We can measure the explained variance by considering the quantity![[Pasted image 20221027173848.png]][3]

[[Clustering]]

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


---
## Footnotes
Backlink: [[AIN Outline]]

Sources:
1. 
	- Name: Example Application Principle Component Analysis
	- Author: Frederik Mallmann-Trenn
	- Date: 27/10/22
2. 
	- Name: Rotations and Eigenstuff
	- Author: Frederik Mallmann-Trenn
	- Date: 27/10/22
3. 
	- Name: PCA Algorithm
	- Author: Frederik Mallmann-Trenn
	- Date: 27/10/2