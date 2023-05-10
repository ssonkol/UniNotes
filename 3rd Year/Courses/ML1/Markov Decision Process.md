# Markov Decision Process
---

## Notes
The overall problem the agent faces here is a Markov decision process (MDP). 
- Mathematically we have
	- a set of states s in S with an initial state s0
	- a set of actions A(s) in each state
	- a transition model P(s' | s, a)
	- a reward function R(s).

Captures any fully observable non-deterministic environment with a Markovian transition model and additive rewards.


A solution is a policy, which we write as pi. It represents a mapping from perceived states of the environment to actions to be taken in those states.

---
Backlink: [[Reinforcement Learning]]
