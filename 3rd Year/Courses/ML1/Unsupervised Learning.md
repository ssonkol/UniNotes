# Unsupervised Learning
---

## Notes
This is when there is no labelled or annotated data.

We look for patterns or interesting structures within the data. (Think of clustering)

You can refer to this [[Clustering]] module here for further information

### Parametric vs Non-Parametric

If the Machine Learning Technique makes an assumption about the structure of the data then it is **Parametric** if not, it is **Non-Parametric**.

- Parametric models can be computationally simpler (Linear Regression)
	- But assumptions that are made can lead to inaccuracy
- Non-Parametric models are more flexible (no assumptions)
	- But they can be intractable for large datasets

### K-Nearest Neighbour (KNN)

Video: https://www.youtube.com/watch?v=4HKqjENq9OU&ab_channel=Simplilearn

This is a simple non-parametric classifier which uses proximity to make classifications or predictions about the grouping of an individual data point.

KNN works by finding the distances between a query and all the examples in the data, selecting the specified number examples (K) closest to the query, then votes for the most frequent label (in the case of classification) or averages the labels (in the case of regression)

The simplest version chooses the class with the most points in the k nearest set.
Whereas a more sophisticated version uses the k nearest points to estimate the probability of a class membership.

KNN classifiers are simple and can work well but they scale badly as they don't work well with high dimensional inputs.

#### The Curse of Dimensionality
The more features means the more examples we need to determine how the features distinguish otherwise we overfit.

We can address this using parametric models
 - Make some assumption about the best way to distinguish between examples
	 - Assume something about the way examples are distributed/generated

---
Backlink: [[Introduction to Machine Learning]]