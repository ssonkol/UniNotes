# Bayes Theory
Tag: #review 

---
## Notes

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


### Bayes' Rule & Conditional Independence

Naïve Bayes is an oversimplified probability model that relies on the idea that in many cases the "effect" variables aren't actually conditionally independent given the cause variable.

Example:
> - *Cause*: it rained yesterday
> - *Effect1*: the streets are wet this morning
> - *Effect2*: I’m late for my class
> If the streets were still wet, then an accident was more likely to happen and the caused traffic jam could be a reason for being late

![[Pasted image 20221012184947.png]][2]
 But we can visualise this as...

![[Pasted image 20221012185210.png]][2]

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