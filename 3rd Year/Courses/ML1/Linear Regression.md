# Linear Regression
---

## Notes
This is learning a linear function of continuous inputs![[Pasted image 20230123230256.png]]
Where we want to estimate values of w0 and w1 from data.

To find the line we find the [w0,w1] that minimise the loss/error![[Pasted image 20230123230404.png]]

### Cost function
This is a plot of the cost vs the function h
![[Pasted image 20230123230627.png]]


#### Gradient Descent Algorithm
1. Start with some initial values for w0 and w1
2. Keep changing these values so that the cost/loss function J(hw) is reduced
3. Continue until you reach minimum
![[Pasted image 20230123230747.png]]

We update with 
![[Pasted image 20230123230811.png]]
where alpha is how big of a step we take downhill.

At the minimum point the equation will equal 0 ![[Pasted image 20230123230910.png]]

##### Batch Gradient Descent
Here we
- Consider all training examples simultaneously
- At each step we consider all the training examples and update the weightings using
	![[Pasted image 20230123231021.png]]

This is guaranteed to converge but it can be slow since we need to compute for all N examples at each step.

##### Stochastic Gradient Descent

We can just do:
![[Pasted image 20230123231127.png]]
for each of the N exampled in turn

Whilst it is often quicker:
- It may not converge is the learning rate is constant
	- Can often be made to converge by decreasing the learning rate over time

##### Multivariate linear regression
With more variables we can simplify the handling of weights by creating a dummy attribute to pair with w0.

Then the formula below is just the weighted sum of all variable values![[Pasted image 20230123231358.png]]

Thus we learn by doing gradient descent as before (choose batch or stochastic gradient descent).

But we need to take overfitting into account and the complexity of the model.
To do this, we add a regularisation term to the loss function ![[Pasted image 20230123231531.png]]
where![[Pasted image 20230123231542.png]]
Lambda is the regularisation parameter : the trade-off between fitting the data and having a simple function.

Then we use Loss'(h) when computing the weight updates.

### Linear Classifiers

These can turn a linear function into a classifier.
- The function defines the decision boundary that separates the two classes.
- A linear decision boundary will separate two linearly separable classes 
- Then classify based on where a point lies in relation to the line.

![[Pasted image 20230123233123.png]]

#### Steps
1. Use the decision rule on an example
2. If it classifies correctly, do not update weights
3. Otherwise update weights as before

Note that it performs worse if data is noisy.
Furthermore if the curve is not smooth then that means the boundaries are hard therefore they can misclassify a lot for examples even a long way into learning.

#### Logistic Regression
The classifier always predicts 0 or 1, even for examples that are very close to the boundary.
We may need to soften the threshold function to get more gradated predictions. This way we can approximate the hard threshold with a continuous function.

Use logistic function as a threshold: ![[Pasted image 20230123233441.png]]
The function taxes one's calculus but the update rule is quite simple ![[Pasted image 20230123233524.png]]
using cross-entropy loss function.

---
Backlink: [[Inductive Learning]]
