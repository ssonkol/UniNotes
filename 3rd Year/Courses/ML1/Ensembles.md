# Ensembles
---
## Notes 

Every classifier will always misclassify some examples.
Hence using an ensemble is an easy way to improve this.

1. Take N classifiers and use them all on the same example
2. Have them vote on the classification
	1. For a binary classification and 5 classifiers, error rate drops from 10% to less than 1%

### Boosting

Boosting extends the idea of an ensemble as it builds on the idea of a weighted training set

Higher weighted examples are counted as more important during training.

1. Start with examples of equal weight and learn classifier h1
2. Test it
3. Increase weights of the misclassified examples and learn a new classifier h2
4. Repeat

The final ensemble is a combination of all the classifiers weighted by how well they perform on the training set.

### AdaBoost

This a commonly used approach to boosting.
Given an initial classifier that is slightly better than random. AdaBoost can generate an ensemble that will perfectly classify the training set.

### Bagging
From the training set D we create multiple training sets:
From each of them we learn a classifier

To classify an example, combine the results of the ensemble
- The Di are separated from D
- Results in multiple sets with the same properties

### Combining Results
- Typical combination is done by voting
- You can also combine regression ensembles by averaging
- Both can be weighted for boosting

### Random Forest

This is Bagging applied on decision trees
- Plus random selection of features for each tree
	- Bagging at feature level

#### Random Subspace Method

Features are selected randomly with replacement between trees.
This is called Random Subspace Method
We can apply it to other kinds of ensemble

---
Backlink: [[Inductive Learning]]
