# N-Armed Bandits
---

## Notes
This means n actions to choose from.

It refers to a hypothetical scenario where you are faced with n slot machines (often called "one-armed bandits"), each with a different probability of paying out a reward when you pull their level. You can think of these probabilities as the arms of the bandits.

The challenge is to figure out which machine has the highest pay-out rate, and then maximise your total reward by playing out that machine repeatedly.

The catch is that you don't know the true pay-out probabilities of each machine beforehand, so you have to explore different machines and learn from the outcomes of your choices over time.

N-armed bandits are often used as a simplified model for more complex decision-making problems in fields such as finance, marketing and AI

### Mathematical format

Action values: After each play at a(t), you get a reward r(t), where: ![[Pasted image 20230308123922.png]]
#### Exploration vs Exploitation
Suppose we form action value estimates Q_t(a) which estimates Q*(a).

The greedy action (one action whose estimated value is greatest at any time step) at t is ![[Pasted image 20230308124128.png]]

- Picking a_t* is exploitation
	- Exploitation maximises the expected reward on one step but exploration may produce the greater total reward in the long run
		- You can't exploit all the time
		- You can't explore all the time
- Picking a_t != a_t* is exploration


You can never stop exploring but you should eventually reduce exploring.

### Action Value Methods

#### Sample Average Method
Maintain a list of all rewards received and average them for each action.

If by the t-th play, action a had been chosen k_a times prior to t, yielding rewards r_1, r_2,... , r_ka then:  ![[Pasted image 20230308124603.png]]
if k_a = 0, set Q_t(a) to some default value e.g. 0
![[Pasted image 20230308125506.png]]

If we go on for long enough, we will converge to the actual value of Q*(a).

The only issue is that this method uses too much memory. Instead, use an incremental implementation.

##### Incremental Implementation
If Q_k is the average of the first k reward and r_k+1 is the k+ 1th reward then:
![[Pasted image 20230308125647.png]]

#### e-greedy

Given an estimate of a reward for each action, we then have to decide what to do.
Greedy action selection always exploits current knowledge to maximise immediate reward, but we don't want to just exploit, e-greedy gives us a way to balance exploration-exploitation.

e-greedy can be denoted as: ![[Pasted image 20230308125858.png]]

##### Method
1. Pick e << 1
2. e-greedy action selection:![[Pasted image 20230308130030.png]]

Most of the time be greedy but explore sometimes.

This is the simplest way to try to balance exploration and exploitation.

#### 10-armed testbed

Bandit with n=10 possible action

Each Q*(a) is chosen randomly from a normal distribution![[Pasted image 20230308130206.png]]
each r_t is also chosen from a normal distribution:![[Pasted image 20230308130231.png]]

The 10-armed testbed: 1000 plays and 2000 randomly generated 10-armed bandit tasks

**over time**

epsilon = 0

![[Pasted image 20230308130350.png]]

A greedy agent, levels off at an average reward of about 1
It finds the optimal action in approximately 1/3 of the tasks

epsilon = 0.1
![[Pasted image 20230308130454.png]]

When exploring more, it find the optimal solution earlier

epsilon = 0.01
![[Pasted image 20230308130619.png]]
It improves more slowly, and eventually performs better than the epsilon = 0.1


#### SoftMax
e-greedy makes a random choice among non-optimal actions.
- Sometimes, it's good not to pick actions with poor outcomes.
- SoftMax picks non-optimal actions based on their reward

Commonly uses the Gibbs distribution to pick the action
Choose action a on the r-th play with probability:![[Pasted image 20230308130811.png]]
where T is the temperature.

When the temperature is high, all actions are approximately equally likely.
As the temperature tends to 0, action selection tends to be greedy selection.
It can vary T over time - high to start, low as the agent thinks it is converging.








---
Backlink: [[Reinforcement Learning]]
