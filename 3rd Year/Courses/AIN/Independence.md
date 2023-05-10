# Independence
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

 To get efficient probabilistic computations, we need two things:
 1. (Conditional) Independence
 2. Bayes rule

To start off...
A and B are independent if:
- $P(A,B) = P(A)P(B)$

![[Pasted image 20220921125659.png]] [3]
In other words

$P(Toothache, Catch, Cavity, Weather) = P(Toothache, Catch, Cavity) * P(Weather)$
- If you store all values naively, this requires 2 * 2 * 2 * 4 = 32 entries
- You can do it in 31 by leaving one entry empty. This is possible since we know that the probabilities add up to 1
- Using the independence, you can even reduce the 31 values to 10:
	- You store 7 for the 3 dependent variables and 3 for weather which is independent 
	- for $n$ independent biased coins, $2^{n} \longrightarrow n$

#### Conditional Independence
- $P(Toothache, Cavity, Catch)$ has:
	- Three binary values
	- thus $2^{3}$ entries in the joint probability rule
	- But these sum to 1
	- So $2^{3} - 1$ independent entries
	- That's 7 independent entries

However, of I have a cavity, the probability that the probe catches in it doesn't depend on whether I have a toothache:
 - $P(catch|toothache,cavity) = P(catch|cavity)$

The same independence holds if I haven't got a cavity
- $P(catch|toothache,\bar{cavity}) = P(catch|\bar{cavity})$

Catch is **conditionally independent** of *Toothache* given *Cavity* 
- $P(Catch|Toothache,Cavity) = P(Catch|Cavity)$

Therefore we write 
$Catch\perp\!\!\!\perp Toothache | Cavity$

Equivalent statements:
> $P(Toothache|Catch,Cavity) = P(Toothache|Cavity)$
> $P(Toothache|Catch,Cavity) = P(Toothache|Cavity) \odot P(Catch|Cavity)$

We can write out full
$P(Toothache, Catch, Cavity)$
$= P(Toothache|Catch,Cavity) \odot P(Catch,Cavity)$
$= P(Toothache|Catch,Cavity) \odot P(Catch,Cavity)P(Cavity)$

which is:
2+2+1 =5 independent numbers

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