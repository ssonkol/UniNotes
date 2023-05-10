# Adaptive Dynamic Programming
---
## Notes

Adaptive dynamic programming (ADP) is a type of reinforcement learning algorithm that is based on the principle of dynamic programming. Like other reinforcement learning algorithms, ADP involves an agent that interacts with an environment and receives feedback in the form of rewards or penalties. The goal of the agent is to learn a policy that maximizes the expected cumulative reward over time.

ADP algorithms are designed to handle situations where the environment is unknown or where the dynamics of the environment are uncertain. ADP algorithms typically use a combination of offline and online learning to adapt to changing environmental conditions. The offline learning component involves using a fixed dataset of past experiences to initialize the value function and policy, while the online learning component involves updating the value function and policy in real-time based on new experiences.

- The main advantage of ADP over other reinforcement learning algorithms is its ability to handle highly complex environments with many states and actions.
- ADP can also handle non-linear dynamics and non-linear function approximations, which makes it suitable for a wide range of real-world applications.
- It is also typically quicker than direct utility estimation

### Solution
1. List states s_i
2. Each state has a utility estimate associated with it, U(s)
3. Each state has an action associated with it, π(s)
4. Each state action pair has a probability distribution![[Pasted image 20230317152454.png]]over the states S 1 that it gets to from s by doing π(s).

**After Learning**
To get utilities, the agent started with a fixed policy, so it always knew what action to take.
- Having gotten the utilities, it could use them to choose actions.
	- Pick the action with the best expected utility in a given state
	- 



---
Backlink:[[Reinforcement Learning]]