# Decision Trees
---

## Notes

Inductive learning means to learn from examples.

In more relevant terms, it means that a hypothesis is found to approximate the target function over a sufficiently large dataset so that it is also able to function well over unseen examples.

An example looks like this:
![[Pasted image 20230123212150.png]]
Node - represents a test value of a feature for a data point
Leaf Node - Specifies the value to be returned.

Trees can be re-represented as sets of if-then rules

### Learning
Once we pick a feature:
1. If all remaining examples are positive then we are done
2. If all remaining examples are negative, then we are done 
3. If there are some positive and some negative examples. then choose the best feature to split them
4. If there are no examples left, then nothing fits that case
	1. Plurality Classification
		1. In this case we can either randomly pick, set a default value based on the root feature or select the majority node output.
5. If there are no features left but still positive and negative examples, these ones have the same description but different classifications
	1. Can be due to noise
	2. Can be due to unobservability of features
	3. Plurality classification is a simple solution

### Choosing the best feature

Ideally the best feature splits the examples into subsets that are all positive or all negative

### Information & Entropy

We measure the information in a feature by looking at how it reduces entropy (lack of order or confusion).
![[Pasted image 20230123222409.png]]

To calculate Log2 we can use
![[Pasted image 20230123222444.png]]


#### Entropy
Example:
Say we need to pick a class based on positive and negative examples.

The chance of class =1 is ![[Pasted image 20230123222624.png]]
This gives us the probability distribution over classes, and we can compute the entropy of S
![[Pasted image 20230123222701.png]]

Therefore for something like 12 restaurant examples, p = n =6 so the entropy is 1.

Now for c classes 
![[Pasted image 20230123222827.png]]

where pi is the proportion of examples in ci.

#### Information gain

We use attributes or features to split examples into subsets.
So what we can do is measure how good a feature is by looking at our original set S and our new subset Si.

What is the entropy of S and what is the entropy of Si given a specific feature?
The difference in entropy is called the **information gain** ![[Pasted image 20230123223522.png]]

Essentially the feature with the biggest difference is the one that is better.
	We want the feature which leads to the smallest entropy

In terms of positive and negative ![[Pasted image 20230123223806.png]]

### Other metrics for picking attributes
- Looking for information gain has a bias as it favours features that have many values

#### Gain Ratio

One solution is to add a metric that penalises features with lots of information
![[Pasted image 20230123224033.png]]

We then combine this with Gain to get a new metric to get the best feature:![[Pasted image 20230123224111.png]]

#### Gini Impurity
Assign a probability based on the number of examples
The Gini Impurity is the probability of this classification mislabelling a randomly selected example.

![[Pasted image 20230123224251.png]]


The easier application is:![[Pasted image 20230123224313.png]]

And if over two classes:![[Pasted image 20230123224328.png]]
If we then have a feature A that splits S into subsets Si , the Gini impurity of these sets is:
![[Pasted image 20230123224625.png]]

The feature with the lowest Gini Impurity is the best choice.

### Overfitting 
If working with a very small training set or a set that contains noise - then this can lead to overfitting

#### Overfitting prevention - for Decision Trees
1. Stop growing the tree earlier
	1. Don't get to the point of overfitting
2. Allow to possibly overfit, and then prune the tree

The second option is more successful

#### Reduced error pruning
1. Consider every branch in the tree as a candidate for pruning
2. Remove the branch, and make the root of the branch into a leaf
3. Use the pularity classification for examples at that leaf
4. Test the new tree
5. Keep a branch pruned if the pruned tree performs better on some validation set than the original tree
6. Repeat while it is possible to prune a branch and improve performance

##### Issues#
Requires another partition of the data
Now we need:
- Training data
- Pruning data
- Test data

When data is limited, it becomes a problem, so we need to:
1. Build the decision tree as before
2. Create rule set
	1. 1 rule for each path from root to leaf
3. Remove preconditions from rules if that improves their accuracy
4. Sort rules by accuracy and apply them in order/sequence when classifying examples

### Ways to improve decision tree

- Extend method to work with multi-valued features
	- This is when features have many values so we convert them into boolean tests
- Continuous/integer input features
	- Infinite sets of possible values so we identify split points which give the highest information gain
- Continuous output values
	- When trying to predict continuous output values we need to create a regression tree which ends with a linear function




---
Backlink: [[Inductive Learning]]