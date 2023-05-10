# Conditional Probability
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
#### Conditional Probability
Equation definition:
> $P(a|b) = \frac{P(a\wedge b)}{P(b)}$ if $P(b) > 0$

##### Product Rule
$P(a \wedge b) = P(a|b) * P(a)$

##### Chain Rule
This is derived by the successive application of the product rule
$P(a,b,c) = P(a,b)P(c|b,a)$
			   $= P(a)P(b|a)P(c|b,a)$


## Questions
##### Question 1
 ![[Pasted image 20220921122633.png]][2]
###### Answer

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