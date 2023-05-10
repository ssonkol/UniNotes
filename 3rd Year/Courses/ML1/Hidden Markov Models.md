# Hidden Markov Models
---
## Notes
##### Markov Assumption (First Order)
The Markov assumption states that the probability of going to the next state only depends on the current state, and not on the history of how we got to that state.

This is known as a "first order" Markov assumption, because it only considers the current state and not any previous states. A higher-order Markov assumption would take into account more previous states.

### Markov Chain

This is a mathematical model that describes a sequence of events in which the probability of each event depends only on the state of the system in the previous event.
![[Pasted image 20230206205713.png]]

### Hidden Markov Model
A Hidden Markov Model (HMM) is a statistical model that can be used to describe a system in which the state of the system is not directly observable, but instead, only the observations of the system are available.

In an HMM, there are a set of hidden states that describe the underlying process of the system, and a set of observable states or outputs. The transition between hidden states and the observation of the system are modelled using probability distributions.

An HMM is useful when you have a sequence of observations, and you want to determine the most likely sequence of hidden states that generated those observations.

#### General Example
Suppose we want to model the relationship between weather and whether or not we carry an umbrella. The weather can either be sunny (S) or rainy (R), and carrying an umbrella can either be yes (Y) or no (N).

In this scenario, the hidden state is the weather (S or R), and the observable state is whether or not we carry an umbrella (Y or N). Let's say that the transition probabilities between hidden states are:

P(Sunny | Sunny yesterday) = 0.8, P(Rain | Sunny yesterday) = 0.2 (If it was sunny yesterday, there's an 80% chance it will be sunny today and 20% chance it will rain) P(S | R) = 0.5, P(R | R) = 0.5 (If it was rainy yesterday, there's a 50% chance it will be sunny or rainy today)

And the emission probabilities (probabilities of observing an umbrella given a hidden state) are:

P(Y | S) = 0.1, P(N | S) = 0.9 (If it is sunny, there's a 10% chance of carrying an umbrella and 90% chance of not carrying one) P(Y | R) = 0.9, P(N | R) = 0.1 (If it is rainy, there's a 90% chance of carrying an umbrella and 10% chance of not carrying one)

Using these probabilities, we can make predictions about whether or not to carry an umbrella based on a sequence of observations, such as "yesterday it was sunny, and today it is cloudy". To do this, we can use algorithms like the Viterbi algorithm to determine the most likely sequence of hidden states (weather) that generated the observed sequence (carrying an umbrella or not).

The Viterbi algorithm is a dynamic programming algorithm that is used to find the most likely sequence of hidden states (weather) that generated a sequence of observations (carrying an umbrella or not) in a Hidden Markov Model (HMM).

In the weather and umbrella example, the Viterbi algorithm starts by initializing the probability of the most likely sequence of hidden states for the first observation. For example, if the first observation is "carrying an umbrella", the probability of the most likely sequence of hidden states that generated this observation can be calculated as:

P(S | Y) = P(Y | S) * P(S) P(R | Y) = P(Y | R) * P(R)

where P(S) and P(R) are the prior probabilities of the hidden states (weather).

Next, the algorithm iteratively computes the probabilities of the most likely sequence of hidden states for each subsequent observation, given the previous observation. For example, if the next observation is "not carrying an umbrella", the probability of the most likely sequence of hidden states that generated this observation can be calculated as:

P(S | N) = max(P(S | Y) * P(N | S), P(R | Y) * P(N | S)) P(R | N) = max(P(S | Y) * P(N | R), P(R | Y) * P(N | R))

where the "max" operator returns the maximum probability of the two possible previous hidden states (weather) given the current observation (not carrying an umbrella).

Finally, the algorithm finds the most likely sequence of hidden states by tracing back the path of maximum probabilities from the last observation to the first observation. In this way, the Viterbi algorithm can determine the most likely weather conditions (hidden states) that generated the observed umbrella-carrying behaviour (observations).

#### Emission Probability 1 

The emission probability plays an important role in the Viterbi algorithm as it determines the likelihood of observing a particular output (umbrella-carrying behavior) given a hidden state (weather condition). In the weather and umbrella example, the emission probabilities are:

P(Y | S) = 0.1, P(N | S) = 0.9 (If it is sunny, there's a 10% chance of carrying an umbrella and 90% chance of not carrying one) P(Y | R) = 0.9, P(N | R) = 0.1 (If it is rainy, there's a 90% chance of carrying an umbrella and 10% chance of not carrying one)

These probabilities are used to calculate the probabilities of the most likely sequence of hidden states given a sequence of observations. For example, if the first observation is "carrying an umbrella", the probability of the most likely sequence of hidden states that generated this observation can be calculated as:

P(S | Y) = P(Y | S) * P(S) P(R | Y) = P(Y | R) * P(R)

where P(S) and P(R) are the prior probabilities of the hidden states (weather). The emission probabilities are used to calculate the likelihood of observing "carrying an umbrella" given the hidden states "sunny" or "rainy".

In the Viterbi algorithm, the emission probabilities are used to determine the most likely sequence of hidden states given a sequence of observations. The algorithm takes into account both the transition probabilities between hidden states and the emission probabilities to determine the most likely sequence of hidden states that generated the observed outputs.

#### Example 2

This is a similar example and we have our probabilities between it being rainy or cloudy and whether we carry an umbrella or not.
![[Pasted image 20230206210750.png]]

We can use a more formal definition to describe our situation![[Pasted image 20230206211252.png]]
This can be turned into a state transition probability matrix 
![[Pasted image 20230206211323.png]]

Our start and end states are not associated with real observations so $a_{io}$ and $a_{if}$ where we are trying to see how to get into the start state or out of the ned state are undefined.

##### Emission Probability 2
The emission probability plays an important role in the Viterbi algorithm as it determines the likelihood of observing a particular output (umbrella-carrying behaviour) given a hidden state

### HMM tasks
We can use HMMs for
- Labelled learning
	- Given a parallel observation and state sequence 0 and X, learn the HMM parameters A & B
- Unlabelled Learning
	- Given an observation sequence 0 ( and only the set of emitting states Se), learn the HMM parameters A and B
- Likelihood Predictions
	- Given an HMM u = (A, B) and an observation sequence O, determine the likelihood P(0 | u)
- Decoding
	- Given an observation sequence 0 and HMM u = (A, B), discover the best hidden state sequence X

### Hidden Markov Model Calculation Example

Let's take into account a dice HMM:
- Imagine a fraudulous croupier in a casino where customers bet on dice outcomes.
- She has two dice – a fair one and a loaded one.
- The fair one has the normal distribution of outcomes – P(O) 1/6 for each number 1 to 6.
- The loaded one has a different distribution.
- She secretly switches between the two dice
- You don’t know which dice is currently in use. You can only observe the numbers that are thrown.
![[Pasted image 20230206212219.png]]

Now remember we do not know the probability of what numbers will appear with the fraudulent die.

We can make our calculations through observation.
![[Pasted image 20230206212349.png]]

- The top layer is whether the dice was fair or loaded.
- The bottom layer is the number we were given.

We then get our emission and transition probability table
![[Pasted image 20230206212734.png]]

We use the rule that s0 to k0 and sf to kf are given values of 1 and values s0 to kf and sf to k0 are given values of 0.

To calculate the rest:
- Emission Probability- 
	- For F and 1 we do 
		- number of 1s that are thrown with F/number of F
			- 4/11 = 0.36
- Transition Probability -
	- from F to F we do
		- number of transitions from F to F/number of Fs
			- 8/11 = 0.7272... = 0.73


### Decoding
This is the act of finding the most likely hidden state sequence X that explains the observation of O given the HMM parameters u.

This is where we use Vertibi

#### Vertibi expanded
To decode a sequence of observations using the Viterbi algorithm, you need to perform the following steps:

1.  Initialization: Calculate the probability of the most likely sequence of hidden states for the first observation. For each hidden state, multiply the prior probability of the state by the emission probability of observing the first output given that state.
    
2.  Recursion: For each subsequent observation, calculate the probability of the most likely sequence of hidden states that generated the observation. For each hidden state, multiply the maximum probability of the previous hidden states by the transition probability to that state and the emission probability of observing the current output given that state.
    
3.  Termination: Find the most likely sequence of hidden states by tracing back the path of maximum probabilities from the last observation to the first observation.
    
4.  Decoding: The most likely sequence of hidden states is the decoded sequence.


Here's an example:

Suppose we have two hidden states "Sunny" and "Rainy", and two observations "Carrying Umbrella" and "Not Carrying Umbrella". The emission probabilities are:

P(Carrying Umbrella | Sunny) = 0.1, P(Not Carrying Umbrella | Sunny) = 0.9 P(Carrying Umbrella | Rainy) = 0.9, P(Not Carrying Umbrella | Rainy) = 0.1

The transition probabilities are:

P(Sunny | Sunny) = 0.8, P(Rainy | Sunny) = 0.2 P(Sunny | Rainy) = 0.3, P(Rainy | Rainy) = 0.7

The prior probabilities are:

P(Sunny) = 0.6, P(Rainy) = 0.4

Given the sequence of observations "Carrying Umbrella", "Not Carrying Umbrella", we can use the Viterbi algorithm to decode the most likely sequence of hidden states as follows:

1.  Initialization: P(Sunny | Carrying Umbrella) = 0.1 * 0.6 = 0.06 P(Rainy | Carrying Umbrella) = 0.9 * 0.4 = 0.36
    
2.  Recursion: P(Sunny | Not Carrying Umbrella) = max(0.06 * 0.9, 0.36 * 0.3) = 0.0486 P(Rainy | Not Carrying Umbrella) = max(0.06 * 0.2, 0.36 * 0.7) = 0.2592
    
3.  Termination: The most likely sequence of hidden states is found by tracing back the path of maximum probabilities. In this case, it is "Rainy", "Sunny".
    
4.  Decoding: The decoded sequence of hidden states is "Rainy", "Sunny".

### Precision & Recall
We can measure system success using accuracy. But sometimes it’s only one type of instances that we find interesting. We don’t want a summary measure that averages over interesting and non-interesting instances, as accuracy does. In those cases, we use precision, recall and F-measure. 

These metrics are imported from the field of information retrieval, where the difference between interesting and non-interesting examples is particularly high. Accuracy doesn’t work well when the types of instances are unbalanced.

![[Pasted image 20230206214456.png]]


### Significance Testing

How good an algorithm is depends on what the alternatives are.
A baseline is defined as a simpler alternative that serves as a comparison. We are often only interested in the difference between our system over the baseline.

A baseline should represent considerably less effort than your proposed solution.

#### Baseline for HMM
- Random guess of hidden states
	- Only knows how often the HMM is in each state on average
	- Doesn't know anything about sequences or observations

#### Statistical Significance Testing

Null Hypothesis : Two result sets come from the same distribution

1. Choose a significance level (a = 0.01 or 0.05)
	1. E.g. System 1 is (really) equally good as System 2
	2. When we try to reject the null hypothesis with confidence 1- a (99% or  95%)
3. Rejecting the null hypothesis means showing that the observed result is very unlikely to have occurred by chance

#### Sign Test
The sign test uses a binary event model.
Events have binary outcomes:
- Positive: System 1 beats System 2 on this example.
- Negative: System 2 beats System 1 on this example.
- (Tie: System 1 and System 2 do equally well on this example / have identical results – more on this later).
Null hypothesis -> baseline and our system are equally good
- prob of negative outcome = prob of positive outcome
- Counts obey a binomial distribution with a mean of 0.5

How likely is it that our observations could arise in that situation? The probability that (at most) 753 out of 2,000 are negative

#### Binomial Test

Given B(N, p)

If the probability of observing our events under the Null Hypothesis is very small (smaller than our pre-selected significance level α, e.g., 0.01), we can safely reject the Null hypothesis.

The P(X <= k) we just calculated directly gives us the probability p we are after. This means there is only a 1% chance that System 1 does not beat System 2.


#### Two-Tailed vs One-Tailed Test
This is when we are testing the difference in a specific direction:
- System 1 better than System 2 (One-tailed test)

A more conservative, rigorous test would be a non-directional one (though some debate on this!)
- Testing for statistically significant difference regardless of direction (Two-tailed test)
- This is given by 2P(X <= k) (because B(N, 0.5) is symmetric).

#### How to treat Ties
When comparing two systems in classification tasks, it is common for a large number of ties to occur. Disregarding ties will tend to affect a study’s statistical power.

We can treat ties by adding 0.5 events to the positive and 0.5 events to the negative side (and round up at the end).


---
Backlink: [[Probabilistic Models]]
