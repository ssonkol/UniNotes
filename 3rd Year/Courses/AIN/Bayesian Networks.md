# Bayesian Networks
Tag: #review 

---
## Notes
### Bayesian Networks
Bayesian Networks exploit conditional independence to create a more compact set of information
- It is a reasonably efficient computation method for some problems.

Bayesian networks are a way to represent dependencies
- Each node corresponds to a random variable
- The graph has no directed cycles
- Each node has a conditional probability that quantifies the effect of the parent nodes

As we can see A and B are independent yet C is dependent on A and B.
![[Pasted image 20221016155226.png]][1]

We can then represent the knowledge about probabilities using a **conditional probability table** (CPT)

![[Pasted image 20221016155354.png]][1]
i.e. saying:
- Given A= True, B = True, the probability of C is 0.2

Bigger Example:
![[Pasted image 20221016155527.png]][1]

### Semantics
#### Global Semantics
We can calculate full joint distribution as the product of the local distributions
![[Pasted image 20221016155712.png]][2]
I.e. given the Bayesian Network below, compute: $P(j\wedge m\wedge a\wedge -b \wedge -e)$
![[Pasted image 20221016160042.png]][2]
Since we can calculate the full joint distribution as the product of local conditional distributions...
We can apply the chain rule
![[Pasted image 20221016160137.png]][2]
Which gives...
![[Pasted image 20221016160228.png]][2]

#### Local Semantics
In local semantics, a Node X is conditionally independent of its non-descendants given its parents. 
![[Pasted image 20221016160338.png]][2]
##### Markov Blanket
In the Markov Blanket theory, each node is conditionally independent of all others given its Markov Blanket:
Parents + child + children's parents
![[Pasted image 20221016160456.png]][2]

Another example of this: 
![[Pasted image 20221016160534.png]][2]
It's Markov Blanket is:
B,C,E,F,G

### Constructing Bayesian Networks
We can build Bayesian Networks like any other form of knowledge representation
1. First figure out the variables that describe the world
2. Decide how they are connected
	- By Conditional Independence
3. Then work out the variables in the CPTs

##### Ways of Compressing Further
Since the CPT grows exponentially with the number of parents
- We can use distributions that are defined compactly

Deterministic nodes are the simplest case

$X = f(Parents(X))$ for some function $f$

example:
$NorthAmerican \Leftrightarrow Canadian\land{US}\land{Mexican}$

You are North American if you are from the US, Canada or are Mexican (*arguable but this was an example of the slides*)

### Inference 
#### Inference by Enumeration
We can evaluate a network by using the structure of the network to tell us which sets of joint probabilities to use.

This gives us a way to sum out variables from the joint without actually constructing its explicit representation.

Given the burglary network:
![[Pasted image 20221016160042.png]][2]

We can make a simple query on the network.

1. Apply Bayes' Rule
2. Note that alpha is $\frac{1}{P(j,m)}$
3. Use the graph to see that we need e, a to get the values of j, m and B
![[Pasted image 20221016161633.png]][3]

4. Use chain rule to expand the expression out
5. Evaluate the expression by going through the variables in order
	1. Multiplying the CPT entries along the way
![[Pasted image 20221016162731.png]][3]


The only issue is that at each point, we need to loop through the possible values of the variable.
- This involves a lot of repeated calculations

Once complete, you can form an ==**Evaluation Tree**==
![[Pasted image 20221016163031.png]][3]

##### Enumeration Algorithm
![[Pasted image 20221016163110.png]]
![[Pasted image 20221016163121.png]][3]
### Prior Sampling

#### Stochastic Simulation
Given by example:

Given a 20 sided die
P(die shows 7) =?

1. Take $n$ random samples from the network
2. Let $X_i$ be the binary r.v. that is 1 if the event sampled in the $i^{th}$ run is 7
3. Output:
	![[Pasted image 20221016163610.png]][4]

The law of large numbers says that the closer you get to n samples, the closer it is to the true value of P 
![[Pasted image 20221016163655.png]][4]

So this can be done with any probability problem - even with a Bayesian Network tree.
#### Prior Sampling

Now with Prior Sampling, we take a list of randomly generated numbers and put them in a run.

Take the example of this Bayesian Network -
![[Pasted image 20221016163901.png]][4]

Random Generated Numbers: 0.4, 0.2, 0.71, 0.2

1. We go in the order of left to right
	1. $P(Cloudy) = 0.5$ and since the sample value $0.4<0.5$ then we can say $P(C) = True$
	2. $P(S|C) = 0.1$ and since the sample value $0.2>0.1$ then we can say $P(S|C) = False$
		1. Remember it's that C is true
	3. $P(R|C) = 0.8$ and since the sample value $0.71<0.8$ then we can say  $P(R|C) = True$
	4. $P(W|S,R) = 0.9$ and since the sample value $0.2<0.9$ then we can say  $P(W|S,R) = True$

So we get the result {Cloudy = true, Sprinkler = false, rain = true, WetGrass = true}

We write {true, false, true, true}

If we then run this process many times, we can count the number of times the above is the result then the proportion of this to the total number of runs is:

$P(c, -s, r,w)$

- The more runs, the more accurate the probability

##### Prior Sampling Function
![[Pasted image 20221016164926.png]][4]

### Rejection Sampling

This is where we:
1. Generate samples (using prior sampling)
2. If the sample is such that e holds 
	- Use it to build an estimate
3. Else
	- Ignore it

#### Rejection Sampling Function

![[Pasted image 20221016165255.png]][5]

#### Pros & Cons of Rejection Sampling

##### Pros
- More efficient than prior sampling

##### Cons
- May have to wait a long time to get enough matching samples
- Still inefficient


Example of inefficiency:

Say we wish to estimate $P(C|A)$ given -

![[Pasted image 20221016165447.png]][5]

Just looking at the network, we would have to reject 80% of all samples...
- Since the probability that A is true is 0.2 then only 20% of all cases would count as valid

#### Likelihood Weighting

This is a version of **Importance Sampling**
1. Fix evidence variable to be true, so just sample relevant events
2. Have to weight them with the likelihood that they fit the evidence
3. Use these probabilities we know to weight the samples

Example:

Given the following network - 
![[Pasted image 20221016165821.png]][5]

If we wanted to know $P(Rain|Cloudy = true, WetGrass = true)$

1. We pick a variable ordering, say:
	**Cloudy, Sprinkler, Rain, WetGrass**
	as before
2. Set the weight $w = 1$ and start 
3. Deal with each variable in order

Remember we want $P(Rain|Cloudy = true, WetGrass = true)$
Cloudy is true so 
![[Pasted image 20221016170051.png]][5]

- Cloud = true, Sprinkler =?, Rain = ?, WetGrass = ?
- $w = 0.5$

Next the Sprinkler... 
Since it is not an evidence variable, we don't know whether it is true or false - so we can pick any assumption (let's just say it returns false this time)
Then...

- Cloud = true, Sprinkler = false, Rain = ?, WetGrass = ?
- $w = 0.5$
	- $w$ doesn't change since Sprinkler wasn't an evidence variable

Next the Rain... 
Since it is not an evidence variable, we don't know whether it is true or false - so we can pick any assumption (let's just say it returns true this time)
Then...

- Cloud = true, Sprinkler = false, Rain = true, WetGrass = ?
- $w = 0.5$
	- $w$ doesn't change since Rain wasn't an evidence variable

Lastly WetGrass
This is an evidence variable with the value true, so we set 
![[Pasted image 20221016170502.png]][5]

That's $0.5 * 0.9 = 0.45$

Then
- Cloud = true, Sprinkler = false, Rain = true, WetGrass = true
- $w = 0.45$

So that means we end up with the event {true, false, true, true} and a weight of 0.45

To find the probability, we tally up the relevant events, weighted with their weights
- The one just calculated would tally under Rain = true

As before, more samples means more accuracy

##### Likelihood Weighting Functions
![[Pasted image 20221016170937.png]]
![[Pasted image 20221016170949.png]][5]

#### Gibbs Sampling

Gibbs sampling takes a rather different approach to sampling...

We don't generate each sample from scratch, we generate samples by making a random change to the previous sample.


Gibbs Sampling for Bayesian Networks starts with an arbitrary state.
1. Pick a state with evidence variables fixed at observed values
	If we know *Cloudy = true*, we pick that
2. Generate the next state by randomly sampling from non-evidence variable
3. Do this sampling conditional to the current values of the Markov Blanket

The algorithm therefore wanders randomly around the state space... flipping one variable at a time, but keeping the evidence variables 'fixed'.

**Example:**

Consider the query:

P(Cloudy | Sprinkler = true, WetGrass = true)
- The evidence variables are fixed to their observed values
- The non-evidence variables are initialised randomly
therefore 
	Cloudy = true
	Rain = false
The state is therefore:
{Cloudy = true, ==Sprinkler = true==, Rain = false, ==WetGrass = true==}


First we sample Cloudy given the current state of its Markov Blanket
	Markov Blanket: Sprinkler & Rain
So sample from:
P(Cloudy | Sprinkler = true, Rain = false)
Suppose we get Cloudy = false, then the new state is: 
{Cloudy = false, ==Sprinkler = true==, Rain = false, ==WetGrass = true==}


Next we sample Rain given the current state of its Markov Blanket and repeat

This time:
P(Rain | Cloudy = true, Sprinkler = true, WetGrass = false)
Suppose we get Rain = true, then the new state is
{Cloudy = false, ==Sprinkler = true==, Rain = true, ==WetGrass = true==}


Each state visited during this process contributes to our estimate for 
P(Cloudy | Sprinkler = true, WetGrass = true)

Say the process visits 80 states
- In 20, Cloudy = true
- In 60 Cloudy = false
Then - 
![[Pasted image 20221016172429.png]][6]

##### Gibbs Sampling Function
![[Pasted image 20221016172540.png]][6]

##### Gibbs Sampling Mathematically
![[Pasted image 20221016172702.png]][6]




---

## Footnotes
Backlink: [[Probability Theory]]

Sources:
1. 
	- Name: lect03-1 Naïve Bayes and Bayesian Networks.pdf
	- Author: Frederik Mallmann-Trenn
	- Date: 16/10/22
2. 
	- Name: lect03-2 Local Semantics and Markov Blanket.pdf
	- Author: Frederik Mallmann-Trenn
	- Date: 16/10/22
3. 
	- Name: lect03-3 Inference by Enumeration.pdf
	- Author: Frederik Mallmann-Trenn
	- Date: 16/10/22
4. 
	- Name: lect03-4 Prior Sampling.pdf
	- Author: Frederik Mallmann-Trenn
	- Date: 16/10/22
5. 
	- Name: lect03-5 Rejection and Likelihood Sampling.pdf
	- Author: Frederik Mallmann-Trenn
	- Date: 16/10/22
6. 
	- Name: lect03-6 Gibbs Sampling and Summary.pdf
	- Author: Frederik Mallmann-Trenn
	- Date: 16/10/22



