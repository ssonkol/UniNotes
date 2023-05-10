# Planning Under Uncertainty
Tag : #review 

---
## Definitions

## Notes
So we have always ran on the assumption that we know what state we are in.  But what happens if – due to the nature of the problem – we don’t know for sure what state we are in.

- There might be some uncertainty about information in the state, meaning that we could potentially be in two or more different states at the same time.  Given we’re aware of this uncertainty, what action should we be taking in this instance?

- Secondly, there is the issue of whether an action completes as intended.  We have always assumed that the state transition system is deterministic.  Meaning that if we apply action a at state s, we will always get the resulting state s’.  So, what happens if we now have actions for which you don’t know the outcome?  It could be multiple possible outcomes of the same action.  Resulting in non-deterministic actions, meaning we don’t always know how the action is going to turn out.

- Lastly, what if an action is non-only non-deterministic, but also has the capacity to result in effects that only occur in certain circumstances.  This results in non-deterministic effects, where it could be – that with a certain probability – we result in a different set of add or delete effects, based on the outcome of the action.

#### Classical Planning

As learnt in [[Classical Planning Fundamentals]]:
- We assume the state is known
- We assume all states in the problem are known
- We assume we know all actions from the current state
- We assume that a given action will always execute as intended
- We assume that the successor states of action execution are also known

### MDP
#### Markov Chains

Markov Chains are probabilistic transitions between states.
![[Pasted image 20221026210555.png]][1]
- The next State is only determined by probabilistic transition between states
	- **This doesn't factor the history of previous states** (known as the Markov Property)

![[Pasted image 20221026210608.png]][1]

#### Markov Decision Process (MDP)
In the Markov Chain, we’re explicitly acknowledging what actions are tied to state transitions and the probabilities with which they can occur.

This will enable us to denote the probability of successful action outcome in a given state such that it actually reaches the successor state s’ that we originally envisaged.

But also we’re going to have the idea of rewards: rewards are a value that influence the decision making process.  And it’s the use of actions and rewards that distinguish a Markov Chain from an MDP.  Given the actions are now not only giving a sense of intentionality, but also the choice of how you want to try and navigate the state space.  Meanwhile the rewards help motivate the action selection.   So you can see the actions now applied to the Markov chain from before.

- This is a sequential decision making problem for a fully observable but stochastic environment.
- Markov Chain holds, but now with probability of actions between states and rewards for action execution.
- It is reliant on two principles
	- Assume that Markov Property holds for action transitions
	- Probability distributions are stationary and don't change
![[Pasted image 20221026211052.png]][1]

##### MDP Further

- MDP is now built around the transition model: T(s, a, s')
- This is similar to existing state transition, but now encodes $P(s' | s, a)$
- However we need a utility function to determine the value of an action. This will help calculate based on state rewards.
![[Pasted image 20221026211418.png]]![[Pasted image 20221026211445.png]][1]

###### Calculating Total Utility
The total Utility of the agent is the sum of all rewards from all states visited

- Negative rewards incentivises optimality

##### MDP Formally

MDP components for all states $s \in S$
- Transition Model: $T(s, a, s')$
- Initial State of the problem: $s_0$
- Reward Function for given state: $R(s)$

Note that the MDP solution is not a plan of action

The MDP solution is a policy: $\pi$
- For any state $s \in S$, $\pi(s)$ denotes what action should be taken in that state
- This means you can get different resulting solutions from the initial goal state, given the stochastic nature of the environment
- Hence the optimality policy will yield the highest expected utility in a given situation.

If the reward is positive, then it will never want to leave and actively avoids the goal states.

### Solving MDP
If we wish to find the optimal policy($\pi^*$) for the problem it needs to be:
- Complete (covers all states)
- Optimal (gives the best action for state s)
- Stationary (actions dependent only on current state)
- Proper (guaranteed to reach a terminal state)

Our policy should yield an expected utility for a given state following a policy.
![[Pasted image 20221026214545.png]][2]

Consider $\pi^*(S)$ for the problem as $U^{\pi^*}(s)$ 
- Its the expected sum of discounted rewards if the agent is running the optimal policy

Hence, we now have ways of acknowledging reward in the problem space:
- $R(S)$ - The short-term reward when reaching aa given state
- $U(s)$ - The long-term reward of passing through $s$ on the way to the goal

Meaning that our optimal solution is selecting the action with the best expected utility.![[Pasted image 20221026214910.png]][2]

#### Calculating the Optimal Policy

We can calculate a utility as the immediate reward plus the expected utility of the successor, assuming optimal action selection.

For this, we use **The Bellman Equation**:![[Pasted image 20221026215045.png]][2]

##### Example:
![[Pasted image 20221026215138.png]][2]

#### Value Iteration Algorithm
We want to find a way to use The Bellman Equation but also update it the more we explore the problem space

**The Bellman Update Equation**![[Pasted image 20221026215306.png]][2]

Initialise $U(s) = 0 \forall s \in S$, then update $U(s)$ for all states in the problem. As time tends towards infinity, the utility values will reach an equilibrium and stabilise

This process is the **value iteration algorithm**.![[Pasted image 20221026215553.png]][2]

### POMDP

#### Hidden Markov Model
This is the same as the Markov Model but, the Markov Chain is now hidden.

States emit observations with a probability - which we can see.
Based on the observations, we can then guess what state we're in.![[Pasted image 20221026220742.png]][3]

#### Partially Observable Markov Decision Process (POMDP)
In this solutions we model probabilistic transitions between states
- The next state is only determined by probabilistic transition between states
- It doesn't factor the history of previous states but is unsure of what state we are in, relying on observations to build history of states visited.
![[Pasted image 20221026221001.png]][3]

#### MDP Continued

POMPD is comprised of:
- States ($S$), Actions ($A$)
- Transition Probabilities: $P(s'|s,a)$
- Reward accrued: $R(s)$
- A belief vector $b$: The probability distribution of which state we are in
- A sensor model $O(o|s)$ which indicates based on the probability we would have seen an observation in a given state

We rely on the observations to make assumptions of which state we are in.
We then take actions and rely on the subsequent observations to build a belief state.

#### Belief States

A Belief state is the probability distribution over all possible states we could exist in
- **Belief Vector** = State probabilities based on percepts and actions to-date

**Example**

We may start in (1,1), but we need observations to tell us we could be in this state.
E.g. - We're 80% confident we're in (1,1) and 10% confident we're in (1,2) and (2,1)
- I.e. $O(o|s_{11})$ = 0.8
![[Pasted image 20221026221720.png]][3]

#### Calculating Belief from Observation 
Now consider the observation of the robot.

It can see the number of visible walls at the current cell.
- It can't tell their orientation, just their number
- Hence this observation $o$ is only ever 1 or 2
- Observations can also have probabilities of occurring

Hence if you then apply the observation to the sensor model, it will tell us which states we could be in right now.
![[Pasted image 20221026231126.png]]![[Pasted image 20221026231142.png]][3]


The belief state needs to be updated based on actions taken in the world. But given we're unsure of the state we're in and whether action execution is successful, we have to factor that into the belief state update.

Update upon taking action $a$ and observing $o$:
![[Pasted image 20221026231317.png]]

1. The probability that we are likely to see observation $o$ at state $s’$ given action $a$![[Pasted image 20221026231429.png]][3]
2. Multiplied by the sum of probabilities of successful action transition from state s to s’, given the belief state that you were in that state to begin with.![[Pasted image 20221026231500.png]][3]
3. It’s worth acknowledging that alpha is what is known as a normalising constant, that makes the belief state sum up to 1.
Being able to calculate and update the belief state is beyond the scope of this module, but knowing this is how it works is important.

##### Example:
Assuming we have no observations and execute the Up action, and then observe one wall, what's the new belief state?

Assuming $a$ = 1![[Pasted image 20221026231716.png]][3]

The only problem is that the normalisation constant needs to be more useful. Which is why the normalisation factor can be considered as 1/sum of observation probabilities in $s'$ multiplied by the probability of reaching s’ based on action a, given belief state s. By doing this instead, we result in a much stronger set of probabilities for the belief state.

#### Value Iteration for a POMDP

Value iteration for MDPs computes one utility value for each state
- Naturally complexity of model increases as number of states increases
- Ultimately still manageable (O(n))

This doesn't scale to POMDPs
- Because we're not modelling states, but belief states that sit atop the actual states.
- The number of unique belief states borders on infinite.

### Solving POMDP

A smarter approach is not to think of the infinite probability distributions, but instead to think about what our utility is going to be defined as

**Utility for MPD**: Expected reward of the state based upon optimal future actions

**Utility for POMDP**: Expected reward of belied state based upon optimal execution of future actions and processing subsequent observations
- This reduces the problem to a finite space
- Trick is to model the utility of limited horizon plans based on belief state.

Our conditional plans, are sequences of actions that execute based upon expectations of belief state and subsequent perceptions

Our conditional plans run on a limited horizon $h$
- Meaning the plans are of length h

By limiting the horizon, the rewards based on specific actions become linear functions over belief space.

From this we can establish a utility function for that belief state, that is piecewise linear.

#### Example

Consider the problem:
- Two states: $s_0$ and $s_1$
- Reward Values: $R(S_{0)}= 0$ and $R(S_{1})= 1$
- Actions (each with probability of 0.9)
	- Stay: Stays in current state
	- Go: Transitions to other state
![[Pasted image 20221026233006.png]][4]
So if we assume $y$ = 1, and consider simple one-step plans, what is the utility of executing these conditional plans $P$ assuming state $S$![[Pasted image 20221026233021.png]][4]

Given the utility of these fixed plans, we can then determine the expected utility of the belief state, in which we execute the optimal policy of highest expected utility.![[Pasted image 20221026233129.png]][4]

By calculating the utility of the plans between states $S_0$ and $S_1$ we can calculate the piecewise linear utility function of the belief state for $S_1$.

![[Pasted image 20221026233405.png]]![[Pasted image 20221026233423.png]][4]

But how does this scale...?

Extend the process from calculating one-step plans to two-step plans.

This increases the number of possible plans, but it also gives us a richer understanding of the utility curve for the belief state.

However, numerous utilities for different belief states on two-step plans are completely subsumed.
- Dashed lines in b) are suboptimal at all points along the line
- These plans are considered dominated and subsequently removed
![[Pasted image 20221026233654.png]][4]

#### Value Iteration for a POMDP
Value iteration for POMDPs is derived from iterating upon the collection of undominated n-step plans (and the subsequent utility hyperplanes derived from them).

By crafting the set of all undominated plans (depth $d = p-1$) consisting of initial action($a$) and each possible percept ($e$)![[Pasted image 20221026233908.png]][4]

#### Value Iteration Function![[Pasted image 20221026233928.png]][4]

#### Summary
![[Pasted image 20221026234013.png]][4]


## Questions

---
## Footnotes
Backlink: [[Artificial Intelligence Planning Outline]]

Sources:
1. 
	- Name: Planning Under Uncertainty 01 - MDP.pptx
	- Author: Dr Tommy Thompson
	- Date: 25/10/22
2. 
	- Name: Planning Under Uncertainty 02 - Solving MDP.pptx
	- Author: Dr Tommy Thompson
	- Date: 25/10/22
3. 
	- Name: Planning Under Uncertainty 03 - POMDP.pptx
	- Author: Dr Tommy Thompson
	- Date: 25/10/22 
4. 
	- Name: Planning Under Uncertainty 04 - Solving POMDP.pptx
	- Author: Dr Tommy Thompson
	- Date: 25/10/22 