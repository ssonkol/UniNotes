# Performance Measurement
---

## Notes

We can tell if we have learnt well if we can predict y given x.
Hence we compute the misclassification rate on the data we have as examples to learn from (test data). Or the proportion of correctly classified examples.

### Learning Curve
This is the percentage of what we got correct on the test set as a function of training set size.

### Unseen Test Set
Therefore we will need to partition the training set into 3 subsets: training set, validation set and the test set.

- The validation set is for model selection and/or parameter tuning
- The test set to evaluate generalisation performance of the best model according to the validation set

The typical split between the 3 is 80%, 10%, 10%
- We would need to ensure enough data for training but also enough data for tuning and testing

### K-Fold Cross Validation
This is where we;

- Split data into k equal subsets/folds to test on.
- Train k-1 sets and test on the remainder fold only.
- Repeat this k times
	- Remember to test on each fold only once
- The compute misclassification error averaged over all k test folds

The final performance is the average of the performances of each fold.
The average test score is a better estimate of the error rate than a single score

- Common values for k are 5 and 10

#### Model Selection and Parameter Tuning

We can use CV+ separate unseen test sets to measure generalisation performance.

There is no best model for all scenarios, so we have to model selection.

### Accuracy
In general the higher the percentages of things we get right is a good indication of accuracy.
However we need to use a confusion matrix to better understand the labels and which ones are misidentified.

### Precision
This is the number of true positives divided by the sum of true positives and false negatives.
![[Pasted image 20230118183808.png]]

### Recall

A low recall score (<0.5) means **your classifier has a high number of False negatives which can be an outcome of imbalanced class or untuned model hyperparameters**

This is the number of true positives divided by the sum of the true positives and false negatives.
![[Pasted image 20230118183825.png]]

### $F_1$ Score

This balances the precision and recall, weighing them equally
![[Pasted image 20230118183841.png]]

![[Pasted image 20230119175020.png]]


### ROC Curve
Known as the receiver operating characteristic. This shows the trade-off between sensitivity.
Classifiers that give curves closer to the top-left corner indicate between performance. As a baseline, a random classifier is expected to give points lying along the diagonal.
![[Pasted image 20230118182744.png]]


## Summary

![[Pasted image 20230119174010.png]]

Use the above table to identify...

94% & 80% 86
96% & 84% 89


---
Backlink: [[Introduction to Machine Learning]]