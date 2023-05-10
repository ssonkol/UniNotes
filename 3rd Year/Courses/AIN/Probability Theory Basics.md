# Probability Theory Basics
Tag: #review

---
## Definitions
Probability Theory 
> A branch of mathematics concerned with the analysis of random phenomena.

Random Variable
>A numerical outcome of a random phenomenon

Naïve Bayes
>It is a classification technique based on Bayes’ Theorem with an assumption of independence among predictors. In simple terms, a Naïve Bayes classifier assumes that the presence of a particular feature in a class is unrelated to the presence of any other feature.


## Notes
#### Basics
- A probability space (probability model) $\Omega$ is a sample space with an assignment $P(w)$ for every $w \in \Omega$ such that:
	- $0 \le P(w) \le 1$
	- $\sum\limits_{w} P(w) =1$
Example:
> For a typical die 
> P(1) = P(2)= P(3) = … = P(6) = 1/6 

- An event A is ay subset of $\Omega$
	- $P(A) = \sum\limits_{(w \in A)} P(w)$
Example:
>A regular die:
>P(die roll<4) = $P(1) + P(2) + P(3) = \frac{1}{6}+\frac{1}{6}+\frac{1}{6} = \frac{1}{2}$

###### Random Variables
Example:
> Toss a coin 3 Times and let X be the number of Heads
> 	- X is a random variable whose possible values are 0, 1, 2 and 3

###### Propositions
The world can be described as propositions i.e. "It's raining"
- Think of a proposition as the event (set of sample points) where the proposition is true

Example: 
>The set of sample points is $\Omega = {1, 2, 3, 4, 5, 6}$.
>$A(w) = true$ or simply $a$ is the event that the number is odd i.e. {1, 3, 5}
>$B(w) = true$ or simply $b$ is the event that the number is < 4 i.e. {1, 2, 3}
>$a \wedge b$ is given by the sample points in {1, 3}

Therefore a state can be defined as a set of Boolean variables

###### Union & Intersection

$P(a \wedge b) = P(a) +P(b) - P(a \wedge b)$
![[Pasted image 20220921115217.png]] [2]

###### Prior & Posterior Probabilities

**Prior Probability**
Prior (unconditional) probabilities are probabilities given before (prior) to the arrival of any new evidence

**Posterior Probability**
This is when a prior probability has new evidence given

Example:
$P(Cavity = true) = 0.1$  now if we now know they have a toothache
$P(Cavity = true|toothache) = 0.2$ which is now the posterior probability

###### Conditional Probabilities
$P(a|b) = \frac{P(a\wedge b)}{P(b)}$ assuming $P(b) > 0$
![[Pasted image 20220921115856.png]] [2]

###### Probability Distribution Notations
![[Pasted image 20220921121132.png]] [2]
*Note some notations might show it as <0.72, 0.1, 0.08, 0.1>*

- Values must be exhaustive and mutually exclusive (no overlap)
- Values have to sum to 1

---
## Footnote

Backlinks : [[Probability Theory]]

Sources:
1. 
	- Name: lect02 - 1 Uncertainty.pdf
	- Author: Frederik Mallmann-Trenn
2. 
	- Name: lect02 - 2 Probability Basics.pdf
	- Author: Frederik Mallmann-Trenn
3. 
	- Name: lect02 - 3 Independence and Conditional Independence.pdf
	- Author: Frederik Mallmann-Trenn
4. 
	- Name: lect02 - 4 Bayes Rule.pdf
	- Author: Frederik Mallmann-Trenn