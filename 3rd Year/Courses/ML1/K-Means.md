# K-Means
---
## Notes
K-means algorithm is a common method used in machine learning for clustering, which is a type of unsupervised learning where the goal is to group similar data points together based on their similarity or proximity. 

Steps: 

1. Initialization: Start by randomly picking K initial values for the means or centroids of the clusters. These K initial values represent the cluster centres.
    
2. Assigning Data Points to Clusters: For each data point xi in the dataset, calculate the distance between xi and each of the K cluster centres, and assign xi to the cluster whose center is closest to it. This is done by finding the argmin of the distance between xi and each μk (cluster center), denoted as Z_i = argmin|X_i - µ_k|, where Z_i represents the cluster assignment of data point xi.
    
3.  Updating Cluster Centers: After assigning all data points to their respective clusters, update the cluster centers by taking the mean (or average) of all the data points assigned to that cluster. This is done by calculating the mean of the data points in each cluster and updating the cluster center as the new mean value. This step is also known as the "centroid update" or "mean update" step.
    
4.  Iteration: Repeat steps 2 and 3 iteratively until convergence. In each iteration, data points are assigned to the closest cluster, and the cluster centers are updated based on the newly assigned data points. Convergence is typically determined based on a stopping criterion, such as when the change in cluster centers falls below a certain threshold or after a certain number of iterations.
    

The K-means algorithm is a simple but effective method for clustering data points into K clusters based on their similarity or proximity to cluster centers. The algorithm iteratively refines the cluster centers based on the assignment of data points to clusters, until convergence is reached. Note that the notation allows for multi-dimensional data points xi and cluster centers μk, meaning that the algorithm can be applied to data with multiple features or dimensions.

---
Backlink: [[Probabilistic Models]]

