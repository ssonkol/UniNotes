# Reinforcement Learning
---

## Outline

- [[N-Armed Bandits]]
- [[Markov Decision Process]]
- [[Value Iteration]]
- [[Passive Reinforcement Learning]]
- [[Adaptive Dynamic Programming]]
- [[Temporal Difference Learning]]
- [[Active Reinforcement Learning]]
- [[Q-Learning]]
- [[SARSA]]
- [[Function Approximation]]

## Notes
Reinforcement learning is learning what to do to maximise a numerical reward signal.

Essentially an agent is placed in an environment, is given a goal and learns how to behave in this environment by trial and error, using feedback from its own actions and experiences.

The agent needs to know that something good has happened or something bad has happened - this feedback is called a reward or reinforcement.

### Reinforcement Learning Characteristics

**Exploration vs Exploitation**
- Exploration finds more information about the environment and might enable higher future rewards
- Exploitation exploits known information to maximise reward, leading to an immediate reward.

e.g.
- Exploitation : Play the move you believe is best
- Exploration: Play an experimental move


**Evaluative vs Instructive feedback**
- Evaluative feedback  - how good was the action.
	- Doesn't say whether that was the best thing to do
- Instructive feedback - what was the best action
	- Doesn't rate the action taken

**Associative vs Non-associative learning**
- Associative maps inputs to outputs and learns the best output for each input
- Non-associative learns the one best output

Reinforcement learning works with evaluative feedback.


---
Backlink: [[ML1 Outline]]