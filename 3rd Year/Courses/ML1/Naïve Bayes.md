# Naïve Bayes
---
## Notes

### Bayes' Theorem
### Bayes' Rule
The probability that some hypothesis $h$ is true, given that some event $e$ has occurred :
	$P(h|e) = \frac{P(e|h)P(h)}{P(e)}$

Now since

	$P(h|e) = P(e|h)P(h) + P(e|\bar h)P(\bar h)$

We can write this in a form commonly applied:

$P(h|e) = \frac{P(e|h)P(h)}{P(e|h)P(h) + P(e|\bar h)(1-P(h))}$

where variables are binary valued.

Example:
>Given
>	$P(h|e) = \frac{P(e|h)P(h)}{P(e|h)P(h) + P(e|\bar h)(1-P(h))}$
> event = underwear
> hypothesis = partner cheating
> To apply Bayes rule we need:
> - $P(e|h)$
> - $P(e|\bar h)$
> - $P(h)$
> So if 
>  - $P(e|h) = 0.5$
> - $P(e|\bar h) = 0.05$
> - $P(h) = 0.04$
>$P(h|e) = \frac{0.5 *0.4}{0.5*0.4 + 0.5*(1-0.04)}$
>           $= 0.294$


Bayes Rule is useful for assessing diagnostic probability from causal probability.

i.e.

$P(Cause|Effect) = \frac{P(Effect|Cause)P(Cause)}{P(Effect)}$

### Bayesian Learning
In some cases we can assume that for every hypothesis is equally likely to the new hypothesis where we may have received new information.

This way we only need to calculate the likelihood.

### Naïve Bayes Classifier

This is a simple but effective practical approach to Bayesian learning.
- It is particularly resistant to overfitting

As a classifier it fits the mould of : ![[Pasted image 20230130162951.png]]

Where we learn an approximation of the mapping from x to y: 

- y = f(x)

where x is a tuple/vector


#### Steps
1. Assume position doesn't matter
2. Assume that features are conditionally independent given the target v (strong independence assumption)

Thus ![[Pasted image 20230130163231.png]]
- p(aj | vi) means - Look for all the cases in which vi occurs and then compute the proportion which have aj

- This means we don't need as much data and can still be accurate

After calculating the p(vi) and the p(aj | vi), we can make predictions about the vi for a give set of x.

When the assumption about conditional independence is satisfied
- Vnb = Vmap

Otherwise if the assumption about conditional independence is not satisfied Vnb is often a good solution.

### Estimating Probabilities
![[Pasted image 20230130165501.png]]

- n is total number of cases where B = b; and 
- n$_c$ is the number of those cases where A = a.
- p is a prior estimate (before taking any data into account).
- Typical value of p is 1/k if the feature has k values.
- m is a constant, equivalent sample size.
	- Weight given to the prior.
		- Can also use other, more sophisticated priors when appropriate.





---
Backlink: [[Probabilistic Models]]
